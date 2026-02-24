# TIPS OID and Tax Reference

## Dependencies

**Requires:** 2.1_TIPS_Basics.md (ref CPI formula, index ratio, adjusted principal), TaxationOfTreasuries.md (TIPS OID tax treatment overview)

**Adds:** OID calculation detail, broker 1099 reporting differences, cost basis step-up, online statement field interpretation, data sources, verification workflow.

---

## Data Sources — Always Fetch, Never Guess

| Data needed                                                               | Source                                                                     |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Daily ref CPI values                                                      | `https://pub-ba11062b177640459f72e0a88d0261ae.r2.dev/TIPS/RefCpiNsaSa.csv` |
| Dated-date ref CPI, issue-date ref CPI, unadj price, accrued int per 1000 | `TipsAuctionResults.csv` (project file)                                    |

Use full-precision ref CPIs — no rounding. Never use index ratios from TreasuryDirect XML/PDF for broker OID verification (TD rounds to 5 decimal places and uses 12/31 not 1/1 as year-end).

---

## Purchase Cost Formula

For auction purchases (original or reopening), all inputs from `TipsAuctionResults.csv`:

```
adj_cost    = face × IR(issue_date) × (unadj_price / 100)
accrued_int = face × (adj_accrued_int_per1000 / 1000)
total_paid  = adj_cost + accrued_int
```

Match the correct CSV row by CUSIP **and** issue date — multiple rows exist per CUSIP for original auction plus reopenings.

---

## OID Calculation

Per IRS Pub 1212, annual OID = inflation-adjusted principal on 1/1 of following year minus inflation-adjusted principal on first day held during the year.

```
annual_OID = face × (IR(1/1 next year) - IR(first day held))
           = face × (refCPI(1/1 next year) - refCPI(first day held)) / refCPI_datedDate
```

### Vanguard — Monthly Breakdown

Vanguard subdivides the annual OID into monthly rows per tax lot, shown in the 1099-OID detail section. Formula for each row:

```
OID = face × (refCPI_end - refCPI_start) / refCPI_datedDate
```

**Period structure:**

- Row 1: settlement date → 1st of following month
- Rows 2–11: 1st of month → 1st of next month
- Final row: 12/1 → 1/1 of following year
- If sold/matured during year: final row ends on that settlement/maturity date

Row 1 may be slightly negative if settlement is near month-end and ref CPI interpolation dips — normal, not an error. Rows sum to the Box 8 total within $0.01 (rounding accumulation).

### Broker Comparison

| Broker         | Breakdown              | Year-end date | Precision                      |
| -------------- | ---------------------- | ------------- | ------------------------------ |
| Vanguard       | Monthly rows per lot   | 1/1 ✓         | Full ref CPI                   |
| Fidelity       | Single total per CUSIP | 1/1 ✓         | Full ref CPI                   |
| TreasuryDirect | Annual only            | 12/31 ❌       | IR rounded to 5 decimal places |

TD 1099-OID is calculated incorrectly per IRS Pub 1212 — always recalculate if using TD figures.

---

## Cost Basis Step-Up

All brokers step up TIPS cost basis annually by the OID reported on 1099-OID, so that OID already taxed as ordinary income is not taxed again as capital gain at disposition.

```
original_cost  = face × IR(settlement) × (unadj_price_at_purchase / 100)
cumulative_OID = face × (IR(today) - IR(settlement_date))
adjusted_basis = original_cost + cumulative_OID
```

The capital gain/loss shown on broker statements = market value − adjusted basis, reflecting only price appreciation above the inflation-adjusted basis. This is correct and not double-counting OID.

Small discrepancies (a few dollars on $100K face) between calculated and displayed basis are normal due to internal IR precision differences.

---

## 1099 Items for TIPS in Taxable Accounts

| Form                | Box | What it is                                   | State exempt?      |
| ------------------- | --- | -------------------------------------------- | ------------------ |
| 1099-OID            | 8   | Annual inflation accrual                     | Yes                |
| 1099-INT            | 3   | Semi-annual coupon interest                  | Yes                |
| 1099-INT supplement | —   | Accrued interest paid at purchase (negative) | Offsets Schedule B |
| 1099-B              | —   | Gain/loss at sale or maturity                | Varies             |

Accrued interest paid at purchase offsets the first coupon on Schedule B. Broker notes it in the supplement but does not report it to IRS — must be entered manually.

---

## Vanguard Online Statement — TIPS Field Definitions

| Field                              | Meaning                           | Formula                             |
| ---------------------------------- | --------------------------------- | ----------------------------------- |
| Price                              | Unadjusted quoted price           | —                                   |
| Current balance                    | Inflation-adjusted market value   | `face × (unadj_price/100) × IR`     |
| Remaining balance                  | Inflation-adjusted principal      | `face × IR`                         |
| Inflation factor / Dec factor TIPS | Index ratio                       | `refCPI(date) / refCPI(datedDate)`  |
| Accrued interest                   | Accrued coupon since last payment | `face × IR × couponRate × days/180` |
| Total cost (cost basis)            | OID-adjusted basis                | `original_cost + cumulative_OID`    |
| Cost per share                     | Adjusted basis per $1 face        | ≈ current IR                        |
| Long-term capital gain             | Price appreciation only           | `market_value − adjusted_basis`     |

---

## Verification Workflow

1. Identify CUSIP → look up in `TipsAuctionResults.csv`: dated date, `ref_cpi_on_dated_date`, issue date, `unadj_price`, `adj_accrued_int_per1000`.
2. Fetch ref CPI CSV for all daily values needed.
3. Calculate from formulas above.
4. **If a row doesn't match:** work backwards — `implied_refCPI_end = (OID × refCPI_datedDate / face) + refCPI_start` — then look up that value in the CSV to identify the correct end date. Do not guess dates.
5. Never assume broker is wrong before verifying your own inputs.

---

## Project File Access Rule

For any content in project files including PDFs: **use `project_knowledge_search` first.** It reads PDFs and all project files. Do not attempt bash-based PDF extraction.
