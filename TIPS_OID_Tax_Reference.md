# TIPS OID and Tax Reference

## Dependencies

**Requires:** 2_1_TIPS_Basics.md (ref CPI formula, index ratio, adjusted principal), TaxationOfTreasuries.md (TIPS OID tax treatment overview)

**Adds:** Regulatory basis for 1099 reporting, qualified stated interest definition, OID calculation detail, amortized bond premium (ABP) calculation, broker 1099 reporting differences, cost basis step-up, online statement field interpretation, data sources, verification workflow.

> **All examples in this document are for illustrative and verification purposes only. Never use hardcoded example values as algorithmic inputs. Always source inputs from `TipsAuctionResults.csv` and the ref CPI CSV as specified in Data Sources.**

---

## Regulatory Basis

### Qualified Stated Interest — Treas. Reg. §1.1275-7(d)

For TIPS subject to the coupon bond method, the regulation defines qualified stated interest as follows:

> "All stated interest on the debt instrument is qualified stated interest. For purposes of this paragraph (d), stated interest is qualified stated interest if the interest is unconditionally payable in cash, or is constructively received under section 451, at least annually at a single fixed rate. **Stated interest is payable at a single fixed rate if the amount of each interest payment is determined by multiplying the inflation adjusted principal amount for the payment date by the single fixed rate.**"

This means each TIPS coupon payment = face × IR(payment date) × (coupon rate / 2), where IR is the index ratio on the payment date. The actual cash coupon paid embeds the inflation adjustment because it is applied to inflation-adjusted principal. This is what is reported in **1099-INT Box 3**.

### Form 1099 Reporting Authority

Per IRS Instructions for Forms 1099-INT and 1099-OID:

> "You may report any qualified stated interest on Treasury Inflation Protected Securities in box 3 of Form 1099-INT rather than in box 2 of Form 1099-OID."

Brokers elect either (a) report QSI on 1099-INT Box 3 and OID on 1099-OID Box 8, or (b) report both on 1099-OID (Box 2 and Box 8). In practice virtually all brokers use option (a).

---

## The Three Taxable Items for TIPS Held in Taxable Accounts

| Form | Box | What it is | Formula | State exempt? |
|---|---|---|---|---|
| 1099-INT | 3 | Semi-annual coupon (QSI) | face × IR(payment date) × coupon/2 | Yes |
| 1099-INT | 12 | Amortized bond premium (ABP) | See below | Reduces Box 3 |
| 1099-OID | 8 | Annual inflation accrual (OID) | face × (IR_end − IR_start) | Yes |

Box 12 ABP only applies if the TIPS was purchased at a premium (adjusted cost > indexed par). It reduces the taxable interest from Box 3 on Schedule B.

---

## Data Sources — Always Fetch, Never Guess

| Data needed | Source |
|---|---|
| Daily ref CPI values | `https://pub-ba11062b177640459f72e0a88d0261ae.r2.dev/TIPS/RefCpiNsaSa.csv` |
| Dated-date ref CPI, issue-date IR, unadj price, accrued int per 1000 | `TipsAuctionResults.csv` (project file) |

Use full-precision ref CPIs — no rounding. Never use index ratios from TreasuryDirect XML/PDF for broker OID verification (TD rounds to 5 decimal places and uses 12/31 not 1/1 as year-end).

---

## Purchase Cost Formula

For auction purchases (original or reopening), all inputs from `TipsAuctionResults.csv`:

```
indexed_par  = face × IR(issue_date)
adj_cost     = indexed_par × (unadj_price / 100)
accrued_int  = face × (adj_accrued_int_per1000 / 1000)
total_paid   = adj_cost + accrued_int
bond_premium = adj_cost − indexed_par   (if positive; zero if purchased at discount)
```

Match the correct CSV row by CUSIP **and** issue date — multiple rows exist per CUSIP for original auction plus reopenings.

---

## Box 3: Qualified Stated Interest (Coupon)

Each semi-annual coupon payment reported in Box 3:

```
coupon_payment = face × (coupon_rate / 2) × IR(payment_date)
```

Where IR(payment_date) = refCPI(payment_date) / refCPI(dated_date).

The Box 3 annual total is the sum of both semi-annual payments. Note: because this is the actual cash received (inflation-adjusted), the payment will vary each period as inflation changes.

---

## Box 8: OID (Annual Inflation Accrual)

Per IRS Pub 1212, annual OID = inflation-adjusted principal at year-end minus inflation-adjusted principal at start of holding period for the year:

```
annual_OID = face × (IR(1/1 next year) − IR(first day held this year))
           = face × (refCPI(1/1 next year) − refCPI(first day held)) / refCPI_dated_date
```

For the first year held, "first day held" = settlement date. For subsequent years, it is 1/1 of that year.

### Vanguard — Monthly Breakdown

Vanguard subdivides the annual OID into monthly rows per tax lot. Formula for each row:

```
OID = face × (refCPI_end − refCPI_start) / refCPI_dated_date
```

**Period structure:**
- Row 1: settlement date → 1st of following month
- Rows 2–11: 1st of month → 1st of next month
- Final row: 12/1 → 1/1 of following year
- If sold/matured during year: final row ends on settlement/maturity date

Row 1 may be slightly negative if settlement is near month-end and ref CPI interpolation dips — normal, not an error. Rows sum to the Box 8 total within $0.01.

### Broker Comparison

| Broker | Breakdown | Year-end date | Precision |
|---|---|---|---|
| Vanguard | Monthly rows per lot | 1/1 ✓ | Full ref CPI |
| Fidelity | Single total per CUSIP | 1/1 ✓ | Full ref CPI |
| TreasuryDirect | Annual only | 12/31 ❌ | IR rounded to 5 decimal places |

TD 1099-OID is calculated incorrectly per IRS Pub 1212 — always recalculate if using TD figures.

---

## Box 12: Amortized Bond Premium (ABP)

Applies only when TIPS is purchased at a premium (adjusted cost > indexed par on issue date). The bond premium is amortized over the life of the bond and reported annually in 1099-INT Box 12 as a reduction of interest income.

### Bond Premium Calculation

```
indexed_par  = face × IR(issue_date)
adj_cost     = indexed_par × (unadj_price / 100)
bond_premium = adj_cost − indexed_par
```

### Amortization Method: Constant Yield (Semi-Annual Periods)

The correct method per §171 uses the constant yield method with semi-annual accrual periods coinciding with coupon payment dates (confirmed by FactualFran and #Cruncher). Day count convention: Actual/Actual (US Treasury standard).

Key inputs:
```
interest_per_period = indexed_par × (coupon_rate / 2)   ← uses indexed par, NOT face
semi_annual_yield   = real_yield_to_maturity / 2
```

Note: the coupon used in the ABP formula is `indexed_par × (coupon_rate / 2)`, not `face × (coupon_rate / 2)`. This reflects the actual QSI payment on inflation-adjusted principal per Reg. §1.1275-7(d), and produces a near-perfect amortization match to the original premium.

**First period (stub):** TIPS are typically issued mid-period. The first coupon period runs from the dated date (COUPPCD) to the first coupon date (COUPNCD).

```
days_in_period      = first_coupon_date − dated_date
days_before_issued  = issue_date − dated_date
days_after_issued   = first_coupon_date − issue_date

accrued_at_issue    = interest_per_period × (days_before_issued / days_in_period)
constant_yield_first = cost × (semi_annual_yield) × (days_after_issued / days_in_period)
ABP_first           = interest_per_period − accrued_at_issue − constant_yield_first
ending_basis        = cost − ABP_first
```

**Subsequent regular periods:**
```
constant_yield  = beginning_basis × semi_annual_yield
ABP             = interest_per_period − constant_yield
ending_basis    = beginning_basis − ABP
```

The sum of all ABP over the life equals bond_premium to within rounding (e.g., 233.864 vs 233.865 for the example below — essentially exact, unlike the flat-coupon approach which left a $0.26 residual).

### Example: CUSIP 91282CEJ6

> **Verification only. All inputs below were sourced from `TipsAuctionResults.csv` and the ref CPI CSV. Do not hardcode these values.**

0.125% 5-Year TIPS | Issued 4/29/2022 | Matures 4/15/2027 | Face $10,000  
Unadj price: 102.328775 | IR on issue: 1.00424 | Real yield: -0.340%  
Indexed par: $10,042.40 | Cost basis: $10,276.26 | Bond premium: $233.86

```
Payment      Box 3 Coupon   Box 12 ABP    Box 8 OID
             (1099-INT)     (1099-INT)    (1099-OID)
-----------  -------------  ------------  ------------
2022-10-15         6.55729      21.92950
   Annual          6.55729      21.92950    511.01626

2023-04-15         6.63966      23.70887
2023-10-15         6.78010      23.66857
   Annual         13.41976      47.37744    342.23245

2024-04-15         6.84682      23.62833
2024-10-15         6.96519      23.58816
   Annual         13.81201      47.21649    282.67724

2025-04-15         7.04652      23.54806
2025-10-15         7.16024      23.50803
   Annual         14.20676      47.05609    351.13109

2026-04-15           (n/a)      23.46807
2026-10-15           (n/a)      23.42817
   Annual            (n/a)      46.89623       (n/a)

2027-04-15           (n/a)      23.38834
   Annual            (n/a)      23.38834       (n/a)

Total ABP                      233.86409
Bond premium                   233.86490  diff=-0.00081
```

Box 3 and Box 8 show n/a for 2026–2027 because ref CPI data is not yet available. Box 12 ABP can be computed through maturity from auction data alone.

ABP figures per #Cruncher and FactualFran; use of `indexed_par × (coupon_rate / 2)` as the per-period coupon produces a near-perfect total match to the bond premium.

### Notes on Broker ABP Reporting

- Brokers may use straight-line rather than constant yield — both methods are permissible under §171, though constant yield is preferred.
- Straight-line produces similar but slightly different annual amounts (e.g., ~$46.98 vs $47.06 for 2025).
- The correct 2025 ABP at $10,000 face for this CUSIP is **$47.056** (~$47). A broker reporting $52 would be in error — $52 corresponds to ~$11,000 face.
- If Box 12 is blank but the supplemental shows a bond premium figure, the broker may have netted it against Box 3 instead — check whether Box 3 equals the gross or net coupon.

---

## Cost Basis Step-Up

All brokers step up TIPS cost basis annually by the OID reported on 1099-OID, so that OID already taxed as ordinary income is not taxed again as capital gain at disposition.

```
original_cost  = face × IR(settlement) × (unadj_price_at_purchase / 100)
cumulative_OID = face × (IR(today) − IR(settlement_date))
adjusted_basis = original_cost + cumulative_OID
```

The capital gain/loss shown on broker statements = market value − adjusted basis, reflecting only price appreciation above the inflation-adjusted basis. This is correct and not double-counting OID.

Small discrepancies (a few dollars on $100K face) between calculated and displayed basis are normal due to internal IR precision differences.

---

## Vanguard Online Statement — TIPS Field Definitions

| Field | Meaning | Formula |
|---|---|---|
| Price | Unadjusted quoted price | — |
| Current balance | Inflation-adjusted market value | `face × (unadj_price/100) × IR` |
| Remaining balance | Inflation-adjusted principal | `face × IR` |
| Inflation factor / Dec factor TIPS | Index ratio | `refCPI(date) / refCPI(datedDate)` |
| Accrued interest | Accrued coupon since last payment | `face × IR × couponRate × days/180` |
| Total cost (cost basis) | OID-adjusted basis | `original_cost + cumulative_OID` |
| Cost per share | Adjusted basis per $1 face | ≈ current IR |
| Long-term capital gain | Price appreciation only | `market_value − adjusted_basis` |

---

## Verification Workflow

1. Identify CUSIP → look up in `TipsAuctionResults.csv`: dated date, `ref_cpi_on_dated_date`, issue date, `unadj_price`, `adj_accrued_int_per1000`, real yield.
2. Fetch ref CPI CSV for all daily values needed.
3. Calculate Box 3 (QSI), Box 8 (OID), and Box 12 (ABP) from formulas above.
4. **If Box 8 doesn't match:** work backwards — `implied_refCPI_end = (OID × refCPI_datedDate / face) + refCPI_start` — then look up that value in the CSV to identify the correct end date. Do not guess dates.
5. **If Box 3 doesn't match:** confirm face value. Box 3 = face × (coupon/2) × IR(payment date). An apparent mismatch often reveals the correct face value.
6. **If Box 12 doesn't match:** check whether broker used straight-line vs constant yield, and whether the starting premium was computed correctly (must use indexed par, not flat par).
7. Never assume broker is wrong before verifying your own inputs.

---

## Project File Access Rule

For any content in project files including PDFs: **use `project_knowledge_search` first.** It reads PDFs and all project files. Do not attempt bash-based PDF extraction.
