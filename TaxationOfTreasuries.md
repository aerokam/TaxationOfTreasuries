# Taxation of Treasury Notes and Bonds, including TIPS

Currently this doc addresses six common scenarios that have been addressed in this thread. It addresses only notes and bonds now, since that was what the questions were about.

**We probably should add info on T-bills as well.**

All Treasury interest is federally taxable at ordinary income rates and exempt from state/local tax. This summary addresses the 6 purchase/disposition scenarios that generate the bulk of annual tax questions here.

---

## Key Concepts (Definitions)

**Coupon interest** — Semi-annual cash payments reported on 1099-INT Box 3. Always taxable in year received. State-exempt.[^pub550-treasury]

**Accrued interest paid to seller** — When you buy between coupon dates, you prepay the seller's earned-but-unpaid interest. Your 1099-INT will include this in Box 3, inflating your reported income. You must subtract it on Schedule B (labeled "Accrued Interest") in the year you receive the first coupon. Your broker notes it in the 1099 supplement but does NOT report it to the IRS — you must track it yourself.[^schb-instructions]

**Market discount** — You paid less than face value on the secondary market (or a reopening), and the discount exceeds the de minimis threshold. Default treatment: tax deferred until disposal, then reported as ordinary interest income (not capital gain) via 1099-B Box 1f at time of disposal. Alternative election: accrue annually as interest income.[^pub550-mdb]

**De minimis discount** — Discount smaller than 0.25% × face value × years to maturity. Treated as capital gain at maturity, not ordinary income. Bonds bought at original auction typically have only a de minimis discount.[^pub550-mdb]

**Market premium** — You paid more than face value. Default: broker amortizes premium and reduces reported coupon interest annually via 1099-INT Box 12 for Treasuries. This reduces taxable interest each year; no capital loss at maturity.[^pub550-premium]

**Accrued market discount (AMD)** — The portion of market discount accrued while you held the bond. Reported in 1099-B Box 1f upon disposal. Treated as ordinary interest income (not capital gain) on your federal return; enters on Schedule B.[^1099b-instructions] State tax treatment varies and is unsettled in many states — most states exempt it as Treasury interest, but consult your state's rules.

**TIPS inflation adjustment (OID)** — Annual increase in TIPS principal due to inflation is "phantom income" — taxable but not received in cash. Reported on 1099-OID Box 8. State-exempt.[^pub1212]

---

## The 6 Scenarios

### Scenario 1: Original Auction → Hold to Maturity (T-Notes/Bonds)

The simplest case. See [Finance Buff: Which Treasury to Buy While Keeping Your Taxes Simple](https://thefinancebuff.com/buy-treasury-simple-taxes.html).

- Each year: coupon interest on 1099-INT Box 3. Import and file. Done.
- At auction, price is typically at a slight discount to par (de minimis). At maturity: tiny capital gain on 1099-B (Schedule D), or broker may fold it into Box 3. De minimis discount is NOT AMD — it is treated as capital gain, not ordinary interest, and carries no state ambiguity.- Accrued interest at purchase: usually zero or negligible at original auction. If nonzero (uncommon), subtract from first coupon year's Schedule B.
- No AMD, no market premium complications.
- State return: Box 3 automatically excluded by most tax software.

### Scenario 2: Reopening Auction → Hold to Maturity (T-Notes/Bonds)

Looks like buying at original auction but has complications. Reopenings are marked with "R" in [Treasury's auction schedule](https://treasurydirect.gov/auctions/general-auction-timing/).[^financebuff-reopen]

- The reopened bond has already been outstanding; you pay accrued interest to Treasury (same mechanics as secondary market accrued interest).
- Your broker's 1099-INT Box 3 will include the full first coupon payment, which overstates your income by the accrued interest you paid.
- Required action: In the year you receive your first coupon, subtract the accrued interest you paid on Schedule B. Your broker notes it in the 1099 supplement ("Taxable accrued Treasury interest paid") but does NOT report it to the IRS — you must track and enter it manually.[^schb-instructions]
- Subsequent years: normal coupon interest on 1099-INT Box 3.
- Price may be at a premium or discount to par depending on rates. If discount > de minimis: AMD applies at maturity (see Scenario 5 below). If premium: broker amortizes via Box 12.
- At maturity: any AMD in 1099-B Box 1f must be moved to Schedule B as interest income (see tax software section below).

### Scenario 3: Original Auction → Sold on Secondary Market (T-Notes/Bonds)

- Annual coupons: 1099-INT Box 3 each year held.
- At sale: 1099-B reports proceeds. Since bought at original auction at/near par, discount is de minimis — any gain/loss on principal is capital gain/loss on Schedule D.
- Accrued interest received from buyer at sale: reported on 1099-INT Box 3 in year of sale; state-exempt.
- No AMD (de minimis discount treated as cap gain, not ordinary income).
- TurboTax tip: Enter 1099-B entries one-by-one (not as sales summary) to properly handle any adjustments.

### Scenario 4: Reopening Auction → Sold on Secondary Market (T-Notes/Bonds)

- Same as Scenario 3 for annual coupons and accrued interest paid at purchase.
- At sale: if you paid a significant premium, amortized premium has reduced your basis — broker adjusts. Capital gain/loss on the remaining principal difference.
- If you paid a discount (bought below par at reopening): AMD accrued during holding period reported in 1099-B Box 1f at sale. Must be reported as ordinary interest on Schedule B (federal), not capital gain. Remaining gain/loss is capital.[^pub550-mdb]
- On Form 8949: use Code D for AMD adjustment. Enter AMD from Box 1f as adjustment in column (g) to convert that portion from cap gain to interest. Also add AMD to Schedule B as "Accrued Market Discount."[^schb-instructions]
- State treatment of AMD: exempt in most states (same rationale as Treasury interest), but not universally settled. States like NY have active debate; states like MI explicitly exempt it. In states that exempt it, you must manually intervene in your tax software — most programs do not automatically transfer AMD to the state exclusion (see tax software section below).

### Scenario 5: Secondary Market Purchase → Hold to Maturity (T-Notes/Bonds)

Most complex scenario for ongoing annual filing.

- Year of purchase: you pay accrued interest to seller. Subtract from Schedule B in year first coupon is received.[^schb-instructions]
- Annual coupons: 1099-INT Box 3 each year.
- If purchased at premium: broker amortizes via 1099-INT Box 12. Reduces taxable coupon interest each year. At maturity: no capital loss (basis has been stepped down by amortization).[^pub550-premium]
- If purchased at discount > de minimis: no annual AMD reporting under default method. AMD accumulates and is reported in 1099-B Box 1f only at maturity.[^pub550-mdb]
- At maturity: 1099-B Box 1f shows total AMD. Report as ordinary interest on Schedule B. The 1099-B will show a capital gain equal to the AMD — you must use Code D on Form 8949 to reclassify it as interest (not cap gain). See tax software section below for how TT and HRB handle this differently.[^1099b-instructions]
- If discount is de minimis: the small gain at maturity is capital gain, not ordinary income.
- State return: coupon interest (Box 3) auto-excluded by most software. AMD requires manual intervention in most software.

### Scenario 6: Secondary Market Purchase → Sold on Secondary Market (T-Notes/Bonds)

All of Scenario 5's complexity, plus capital gain/loss calculation.

- Annual coupons, accrued interest paid, premium amortization: same as Scenario 5.
- At sale: 1099-B shows proceeds and basis. AMD accrued to date of sale is in Box 1f.
- AMD portion → ordinary interest income on Schedule B (Code D on Form 8949).[^schb-instructions]
- Remaining gain or loss above AMD → short-term or long-term capital gain/loss depending on holding period.
- Accrued interest received from buyer at sale → 1099-INT Box 3.
- State AMD uncertainty applies (same as Scenarios 4 and 5).

---

## TIPS — Additional Layer (Applies to All 6 Scenarios)

All of the above applies to TIPS, plus:

- Annual inflation adjustment: reported on 1099-OID Box 8. Taxable as ordinary income federally; state-exempt. This is "phantom income" — you pay tax on it but don't receive cash (the adjustment accrues to principal).[^pub1212]
- Deflation year: if CPI falls, negative OID reduces your taxable income (shown as negative in Box 8 or as an adjustment). Cannot reduce below zero for the year.
- At maturity: you receive the inflation-adjusted principal. No additional tax on the principal increase at that point — it was already taxed annually via OID.
- Acquisition premium on TIPS (secondary market): if you paid more than inflation-adjusted par, that acquisition premium offsets OID each year. Broker tracks this; reported in 1099-OID Box 6.[^pub1212]
- TIPS bought at reopening auction: same accrued interest complications as nominal bonds, plus OID complications. Avoided by buying only at original TIPS auctions and holding to maturity.

---

## Where Things Go — Quick Reference

| Item | Form | Destination | State Handling |
|------|------|-------------|----------------|
| Coupon interest | 1099-INT Box 3 | Schedule B | Auto-excluded by most software |
| TIPS inflation adjustment | 1099-OID Box 8 | Schedule B | Auto-excluded by most software |
| AMD at disposal | 1099-B Box 1f | Form 8949 (Code D) + Schedule B as interest | Manual intervention required |
| Capital gain/loss (non-AMD) | 1099-B | Schedule D | — |
| Accrued interest paid to seller | 1099 supplement only (not IRS-reported) | Schedule B subtraction (manual) | — |
| Premium amortization | 1099-INT Box 12 | Reduces Box 3 interest on Schedule B | — |

---

## Tax Software: How TurboTax and H&R Block Handle AMD Differently

This is where most annual confusion originates. Box 3 (coupon interest) and Box 8 (TIPS OID) flow correctly in both programs. AMD from 1099-B Box 1f is where they diverge.

### TurboTax

**Federal handling:** Enter each 1099-B transaction *one by one* (not as a sales summary). When you enter Box 1f, TurboTax automatically:

- Applies Code D on Form 8949, reducing the capital gain by the AMD amount
- Carries the AMD to Schedule B as "Accrued Market Discount" — ordinary interest income

**Critical: use one-by-one entry, not sales summary.** If you enter as a sales summary total, TT may apply Code D but not carry AMD to Schedule B, causing underreporting of income. Summary-entry adjustments also trigger a requirement to mail a paper statement to the IRS.[^tt-onebyone]

**State handling:** Even when AMD is correctly moved to Schedule B federally, TurboTax typically does *not* automatically carry it to the state Treasury interest exclusion. For states like NY, entering the AMD amount with state code "NY" in the adjustment worksheet does not increase the US Government interest subtraction on the state return. A manual override of the state Treasury interest exclusion line is usually required, adding the AMD to the Box 3 total for state exclusion purposes. This override does not prevent e-filing.[^tt-ny-override]

### H&R Block

**Federal handling:** When you enter the 1099-B with Box 1f AMD, HRB:

- Subtracts the AMD from the capital gain on Form 8949 (Code D), netting gain to zero
- Then warns you that the AMD must also be reported as interest income on a 1099-INT — but does *not* do this automatically[^hrb-dummy]

**Required manual step — the "dummy 1099-INT":** You must create a separate 1099-INT entry in HRB to report the AMD as interest income:

- Create a new 1099-INT with a descriptive payer name such as "Fidelity Treasury Market Discount" (do not call it "Accrued Market Discount" — you didn't accrue it annually, you realized it at disposal)
- Enter the AMD amount in **Box 3** (US Treasury Obligations), NOT Box 1 — this is critical[^hrb-dummy]

**Why Box 3 matters in HRB:** Entering in Box 3 of the dummy 1099-INT causes HRB to automatically treat it as state-exempt Treasury interest and carry it through to the state return correctly. If you enter in Box 1 instead, HRB will tax it at the state level. This is actually an advantage over TurboTax's approach — HRB's workaround, while manual, achieves the correct state result more reliably once you know the procedure.

**HRB import caveat:** If you import a Schwab (or other broker) consolidated 1099 into HRB, the Box 1f AMD may import but the description/memo field may be blank, which can cause capital gains on Schedule D to be overstated. Verify after import.[^hrb-import]

**HRB-specific known bug — Bond Premium + Accrued Interest Paid:** HRB has a longstanding bug (confirmed through at least tax year 2023): when a single 1099-INT has both bond premium amortization (Box 12) and accrued interest paid to seller requiring an adjustment, HRB cannot handle both adjustments on one 1099-INT entry. The workaround is to split the brokerage's 1099-INT into two dummy 1099-INTs, each handling one adjustment, with the Box 3 amounts split between them totaling the correct sum. The IRS matches totals, not individual 1099s, so this is acceptable.[^hrb-bug]

### FreeTaxUSA

For completeness: FreeTaxUSA reportedly handles AMD more automatically — it adds the AMD from Box 1f to Schedule B without requiring a dummy 1099-INT. Whether it correctly identifies it as Treasury interest for state exclusion purposes requires verification by the user.[^ftusa]

### Summary — AMD Handling by Software

| | TurboTax | H&R Block | FreeTaxUSA |
|-|----------|-----------|------------|
| Code D on Form 8949 | Auto | Auto | Auto |
| AMD → Schedule B as interest | Auto (one-by-one entry only) | Manual (dummy 1099-INT) | Auto |
| State Treasury exemption for AMD | Manual override required | Auto if dummy 1099-INT uses Box 3 | Verify manually |

### Bottom Line for Filers

**TurboTax users:** Enter 1099-B bond transactions one-by-one. Verify AMD appears on Schedule B. Then manually check/override your state return to include AMD in the Treasury interest exclusion.

**H&R Block users:** After entering the 1099-B with Box 1f, create a dummy 1099-INT with the AMD amount in Box 3. Verify your 1099-B import didn't leave the capital gain overstated.

**Both:** The IRS matches totals, not individual 1099 line items, so splitting entries across dummy 1099-INTs for mechanical reasons is acceptable and does not trigger issues.

---

## The Finance Buff Principle — Why It Matters

Scenario 1 (and its TIPS equivalent) is the only one requiring no manual adjustments and no AMD/state ambiguity. Everything flows cleanly from Box 3 and Box 8 of the 1099s with no intervention. Every step away from "original auction, hold to maturity" adds at least one manual adjustment: reopenings add accrued interest tracking; secondary market purchases add AMD and state complications; selling early adds AMD plus capital gain splitting. The complexity compounds when all three factors combine (Scenario 6). This is the practical basis for [Finance Buff's advocacy](https://thefinancebuff.com/buy-treasury-simple-taxes.html) of buying at original auction and holding to maturity.

---

## Caveats

- State treatment of AMD on Treasuries is unsettled in several states (notably NY). The dominant view is that AMD, being reclassified as Treasury interest income, should be state-exempt, but no definitive ruling exists in all states. See the extended discussion on NY in this thread and the linked NY-specific thread.
- Tax software behavior can change year to year. Verify your software is handling AMD correctly before filing.
- This is a summary of general principles. IRS Publication 550 is the authoritative source. Consult a tax professional for your specific situation.

---

## References

[^pub550-treasury]: IRS Publication 550 (2024), *Investment Income and Expenses* — "U.S. Treasury Bills, Notes, and Bonds" section. <https://www.irs.gov/publications/p550>

[^pub550-mdb]: IRS Publication 550 (2024), *Investment Income and Expenses* — "Market Discount Bonds" section. <https://www.irs.gov/publications/p550>

[^pub550-premium]: IRS Publication 550 (2024), *Investment Income and Expenses* — "Bond Premium Amortization" section. <https://www.irs.gov/publications/p550>

[^schb-instructions]: IRS Instructions for Schedule B (Form 1040) (2025) — "Accrued Interest" and "Accrued Market Discount" subsections. <https://www.irs.gov/instructions/i1040sb>

[^1099b-instructions]: IRS Instructions for Form 1099-B (2026) — Box 1f (Accrued Market Discount) and Code D. <https://www.irs.gov/instructions/i1099b>

[^pub1212]: IRS Publication 1212 (12/2025), *Guide to Original Issue Discount (OID) Instruments* — TIPS OID reporting, acquisition premium. <https://www.irs.gov/publications/p1212>

[^financebuff-reopen]: Finance Buff, "Which Treasury to Buy While Keeping Your Taxes Simple" — reopening auction mechanics and tax implications. <https://thefinancebuff.com/buy-treasury-simple-taxes.html>

[^tt-onebyone]: Intuit TurboTax community discussion: "Accrued Market Discount on treasury bond" — confirms one-by-one entry required for AMD to flow to Schedule B. <https://ttlc.intuit.com/community/taxes/discussion/accrued-market-discount-on-treasury-bond/00/3463770>

[^tt-ny-override]: Intuit TurboTax community discussion: "Accrued Market Discount on treasury bond" — NY state override required for AMD Treasury exclusion. <https://ttlc.intuit.com/community/taxes/discussion/accrued-market-discount-on-treasury-bond/00/3463770>

[^hrb-dummy]: Bogleheads.org forum, "Reporting accrued interest paid in H&R Block" — Kevin M's description of dummy 1099-INT workaround, Box 3 requirement. <https://www.bogleheads.org/forum/viewtopic.php?t=273370>

[^hrb-import]: Bogleheads.org megathread, "Taxation of Treasury bills, notes and bonds" — HRB Schwab import AMD memo field issue. <https://www.bogleheads.org/forum/viewtopic.php?t=390405>

[^hrb-bug]: Bogleheads.org forum, "H&R Block software bug: tax-exempt interest with bond premium and accrued interest" — Kevin M's documentation of the Bond Premium + Accrued Interest bug and two-1099-INT workaround. <https://www.bogleheads.org/forum/viewtopic.php?t=273011>

[^ftusa]: Bogleheads.org megathread, "Taxation of Treasury bills, notes and bonds" — FreeTaxUSA AMD handling reported by users. <https://www.bogleheads.org/forum/viewtopic.php?t=390405>
