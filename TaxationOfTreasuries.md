# Taxation of Treasury Notes and Bonds, including TIPS

Currently this doc addresses six common scenarios that have been addressed in this thread. It addresses only notes and bonds now, since that was what the questions were about.

The six scenarios are:

- Scenario 1: Original Auction → Hold to Maturity
- Scenario 2: Reopening Auction → Hold to Maturity
- Scenario 3: Original Auction → Sold on Secondary Market
- Scenario 4: Reopening Auction → Sold on Secondary Market
- Scenario 5: Secondary Market Purchase → Hold to Maturity
- Scenario 6: Secondary Market Purchase → Sold on Secondary Market

**We probably should add info on T-bills as well.**

All Treasury interest is federally taxable at ordinary income rates and exempt from state/local tax. This summary addresses the 6 purchase/disposition scenarios that generate the bulk of annual tax questions here.

## Table of Contents

- [Key Concepts (Definitions)](#key-concepts-definitions)
- [The 6 Scenarios](#the-6-scenarios)
- [Filing Checklist by Scenario](#filing-checklist-by-scenario)
- [TIPS — Additional Layer](#tips--additional-layer-applies-to-all-6-scenarios)
- [Where Things Go — Quick Reference](#where-things-go--quick-reference)
- [Tax Software: How TurboTax and H&R Block Handle AMD Differently](#tax-software-how-turbotax-and-hr-block-handle-amd-differently)
- [The Finance Buff Principle — Why It Matters](#the-finance-buff-principle--why-it-matters)
- [Common Mistakes](#common-mistakes)
- [Caveats](#caveats)

---

## Key Concepts (Definitions)

**Coupon interest** — Semi-annual cash payments reported on 1099-INT Box 3. Always taxable in year received. State-exempt.[^pub550-treasury]

**Accrued interest paid to seller** — When you buy between coupon dates, you prepay the seller's earned-but-unpaid interest. Your 1099-INT will include this in Box 3, inflating your reported income. You must subtract it on Schedule B (labeled "Accrued Interest") in the year you receive the first coupon. Your broker notes it in the 1099 supplement but does NOT report it to the IRS — you must track it yourself. At original auction, accrued interest is typically small (a few days or weeks), so the tax impact of missing it is minor. At secondary market purchases or reopening auctions, accrued interest can be large, making it material to get right.[^schb-instructions]

**Market discount** — You paid less than face value on the secondary market (or a reopening), and the discount exceeds the de minimis threshold. Default treatment: tax deferred until disposal, then reported as ordinary interest income (not capital gain) via 1099-B Box 1f at time of disposal. Alternative election: accrue annually as interest income.[^pub550-mdb]

**De minimis discount** — Discount smaller than 0.25% × face value × years to maturity. Treated as capital gain at maturity, not ordinary income. Bonds bought at original auction typically have only a de minimis discount. *Example: A $10,000 bond with 5 years to maturity has a de minimis threshold of $10,000 × 0.0025 × 5 = $125. A discount ≤$125 is de minimis (taxed as capital gain); a discount >$125 triggers ordinary income treatment (AMD).*[^pub550-mdb]

**Amortized bond premium (ABP)** — You paid more than face value. Default: broker amortizes premium and reduces reported coupon interest annually via 1099-INT Box 12 for Treasuries. This reduces taxable interest each year; no capital loss at maturity. Alternative: you can elect NOT to amortize the premium (IRS Form 4952 or similar election depending on your tax software), in which case the premium is treated as a capital loss at maturity. Amortization is almost always optimal for Treasuries because it converts an accrual-basis reduction annually rather than a capital loss (which is less valuable). Rarely, if you have substantial capital gains elsewhere, you might elect not to amortize to avoid losing the benefit of the annual reduction. Consult a tax professional if you want to explore this.[^pub550-premium]

**Accrued market discount (AMD)** — The portion of market discount accrued while you held the bond. Reported in 1099-B Box 1f upon disposal. Treated as ordinary interest income (not capital gain) on your federal return; enters on Schedule B.[^1099b-instructions] State tax treatment varies and is unsettled in many states — most states exempt it as Treasury interest, but consult your state's rules.

**TIPS inflation adjustment (OID)** — Annual increase in TIPS principal due to inflation is taxable but not received in cash. Reported on 1099-OID Box 8. State-exempt.[^pub1212]

---

## The 6 Scenarios

### Scenario 1: Original Auction → Hold to Maturity (T-Notes/Bonds)

The simplest case. See [Finance Buff: Which Treasury to Buy While Keeping Your Taxes Simple](https://thefinancebuff.com/buy-treasury-simple-taxes.html).

- Each year: coupon interest on 1099-INT Box 3. Import and file. Done.
- At auction, price is typically at a slight discount to par (de minimis).
- At maturity: the tiny de minimis discount produces a small capital gain reported on 1099-B (Schedule D), or the broker may fold it into Box 3. De minimis discount is NOT treated as AMD — it is treated as capital gain, not ordinary interest, and carries no state ambiguity.
- The interest accrued between auction date and issue date is small (typically a few days to a couple weeks of coupon interest). *Example: it was $1.91644 per $1,000 for the 20-Year auctioned on 02/18/2026 and issued on 03/02/2026.* Technically, you should subtract it from first coupon year's Schedule B to be accurate. If you forget it, the tax impact is minor because the amount is small—unlike reopenings or secondary market purchases, where accrued interest can be material. The Finance Buff article glosses over this, but the professional approach is to track it.
- No AMD, no market premium complications.
- State return: exact handling depends on the tax software used.

### Scenario 2: Reopening Auction → Hold to Maturity (T-Notes/Bonds)

Looks like buying at original auction but has complications. Reopenings are marked with "R" in [Treasury's auction schedule](https://treasurydirect.gov/auctions/general-auction-timing/).[^financebuff-reopen]

-  You pay interest accrued between the original auction date and the reopening issue date to Treasury (same mechanics as secondary market accrued interest).
- Your broker's 1099-INT Box 3 will include the full first coupon payment, which overstates your income by the accrued interest you paid.
- Required action: In the year you receive your first coupon, subtract the accrued interest you paid on Schedule B. Your broker notes it in the 1099 supplement ("Taxable accrued Treasury interest paid") but does NOT report it to the IRS — you must track and enter it manually.[^schb-instructions]

  > ⚠️ **Critical:** If you don't subtract accrued interest paid on Schedule B, you'll overreport income by that amount and owe tax on money you didn't keep. Brokers don't report this to the IRS, so there's no automatic correction — the onus is entirely on you to track and adjust it.

- Subsequent years: normal coupon interest on 1099-INT Box 3.
- Price may be at a premium or discount to par. If discount > de minimis: AMD applies at maturity (see Scenario 5 below). If premium: broker amortizes via Box 12.
- At maturity: any AMD in 1099-B Box 1f must be moved to Schedule B as interest income (see tax software section below).

#### Quick Comparison: Original Auction vs. Reopening (Both Held to Maturity)

| Aspect | Original Auction | Reopening Auction |
|--------|-----------------|-------------------|
| **Accrued interest at purchase** | Small (days between auction and issue date) | Significant (months/years since original auction date) |
| **Dollar impact if not tracked** | Minor (days of interest) | Major (months+ of interest) |
| **Your 1099-INT Box 3 first coupon** | Slightly overstates by small amount | Notably overstates by accrued interest paid |
| **Schedule B adjustment required** | Yes, but $ amount is small | **Yes — and amount is material** |
| **IRS notification of adjustment** | Broker notes it; IRS doesn't — you track it | Broker notes it; IRS doesn't — you track it |
| **Price at purchase** | At/near par (de minimis discount typical) | At/near par or premium/discount depending on rates |
| **Market discount or premium applies** | Unlikely (de minimis discount only) | Likely (can be substantial AMD or ABP requiring tracking) |
| **Filing complexity** | Low (small adjustment) | Moderate (larger accrued interest + possible AMD/ABP) |
| **Bottom line** | Clean, single small adjustment | More steps; accrued interest amount is the key gotcha |

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

## Filing Checklist by Scenario

**Scenario 1: Original Auction → Hold to Maturity**
- ☐ Received coupon interest each year on 1099-INT Box 3?
- ☐ Small accrued interest at purchase noted and subtracted from first coupon on Schedule B? (Minor impact if missed)
- ☐ De minimis capital gain at maturity on 1099-B reported to Schedule D?
- ☐ Box 3 automatically excluded from state return by tax software?

**Scenario 2: Reopening Auction → Hold to Maturity**
- ☐ Accrued interest from reopening date to issue date tracked (ask broker or Treasury Direct)?
- ☐ Subtracted accrued interest from 1099-INT Box 3 on Schedule B in year of first coupon?
- ☐ Received coupon interest each year on 1099-INT Box 3 afterward?
- ☐ Any AMD at maturity from 1099-B Box 1f moved to Schedule B as interest?
- ☐ Market premium tracked and amortized annually via 1099-INT Box 12?

**Scenario 3: Original Auction → Sold on Secondary Market**
- ☐ Coupon interest received each year on 1099-INT Box 3?
- ☐ Accrued interest received from buyer at sale on 1099-INT Box 3 (year of sale)?
- ☐ De minimis capital gain/loss on principal to Schedule D from 1099-B?
- ☐ Entered 1099-B one-by-one (not summary) if using TurboTax?

**Scenario 4: Reopening Auction → Sold on Secondary Market**
- ☐ Accrued interest at purchase tracked and subtracted on Schedule B (year of first coupon)?
- ☐ Annual coupon interest on 1099-INT Box 3?
- ☐ Accrued interest received from buyer at sale on 1099-INT Box 3?
- ☐ AMD from 1099-B Box 1f moved to Schedule B via Form 8949 Code D?
- ☐ Remaining capital gain/loss (after AMD) to Schedule D?
- ☐ Market premium adjustments tracked?
- ☐ State return adjusted for AMD exemption if applicable?

**Scenario 5: Secondary Market Purchase → Hold to Maturity**
- ☐ Accrued interest paid to seller tracked and subtracted on Schedule B (year of first coupon)?
- ☐ Annual coupon interest on 1099-INT Box 3?
- ☐ Annual premium amortization via 1099-INT Box 12 tracked (reduces taxable interest)?
- ☐ AMD at maturity from 1099-B Box 1f moved to Schedule B via Form 8949 Code D?
- ☐ State return adjusted for AMD exemption if applicable?

**Scenario 6: Secondary Market Purchase → Sold on Secondary Market**
- ☐ Accrued interest paid to seller tracked and subtracted on Schedule B (year of first coupon)?
- ☐ Annual coupon interest on 1099-INT Box 3 each year held?
- ☐ Annual premium amortization via 1099-INT Box 12?
- ☐ Accrued interest received from buyer at sale on 1099-INT Box 3?
- ☐ AMD accrued to sale date from 1099-B Box 1f moved to Schedule B via Code D?
- ☐ Remaining capital gain/loss (after AMD) to Schedule D or Form 8949?
- ☐ Holding period (short-term vs. long-term) confirmed?
- ☐ State return adjusted for AMD exemption if applicable?

---

## TIPS — Additional Layer (Applies to All 6 Scenarios)

All of the above applies to TIPS, plus:

- Annual inflation adjustment: reported on 1099-OID Box 8. Taxable as ordinary income federally; state-exempt. You pay tax on it but don't receive cash (the adjustment accrues to principal).[^pub1212]
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

| Software | Quick Steps | Gotcha |
|----------|-------------|--------|
| **TurboTax** | Enter 1099-B bond transactions one-by-one. Verify AMD appears on Schedule B. Then manually check/override your state return to include AMD in the Treasury interest exclusion. | Summary-entry mode prevents AMD from flowing to Schedule B, causing income underreporting. Always use one-by-one entry. State return requires manual AMD addition — software does not auto-carry it to exclusion. |
| **H&R Block** | After entering the 1099-B with Box 1f, create a dummy 1099-INT with the AMD amount in Box 3. Verify your 1099-B import didn't leave the capital gain overstated. | Box 3 is critical — Box 1 causes state taxation of AMD. If importing Schwab consolidated 1099, verify memo field populated and capital gain not doubled. The Bond Premium + Accrued Interest bug requires splitting into two dummy 1099-INTs. |
| **Both** | The IRS matches totals, not individual 1099 line items, so splitting entries across dummy 1099-INTs for mechanical reasons is acceptable and does not trigger issues. | Don't panic if you create a dummy 1099-INT for workarounds — IRS matches Box totals across all 1099s you file, not individual forms. |

---

## The Finance Buff Principle — Why It Matters

Scenario 1 (and its TIPS equivalent) is the only one requiring no manual adjustments and no AMD/state ambiguity. Everything flows cleanly from Box 3 and Box 8 of the 1099s with no intervention. Every step away from "original auction, hold to maturity" adds at least one manual adjustment: reopenings add accrued interest tracking; secondary market purchases add AMD and state complications; selling early adds AMD plus capital gain splitting. The complexity compounds when all three factors combine (Scenario 6). This is the practical basis for [Finance Buff's advocacy](https://thefinancebuff.com/buy-treasury-simple-taxes.html) of buying at original auction and holding to maturity.

---

## Common Mistakes

- **Forgetting to subtract accrued interest paid on Schedule B.** Your 1099-INT shows the full coupon (including accrued interest you prepaid to the seller), but the IRS doesn't know you paid accrued interest — only you do. Result: overstated income and a tax bill on money you didn't keep. This applies to all reopening and secondary market purchases.
- **Entering AMD in the wrong software field.** In H&R Block, AMD **must** go in Box 3 of a dummy 1099-INT to achieve state exemption. Entering it in Box 1 causes it to be taxed at the state level. In TurboTax, AMD flows correctly to Schedule B via Code D on Form 8949, but you must still manually override the state return.
- **Not verifying state AMD treatment after software import.** Most tax software doesn't automatically carry AMD to the state Treasury interest exclusion. Even if your federal return is correct, your state return may be taxing AMD as ordinary income. Check your state provisions and manually adjust if needed.
- **Assuming all Treasury discounts are de minimis.** Only bonds bought at original auction typically have de minimis discounts. Secondary market purchases at a significant discount trigger AMD rules and ordinary income treatment, not capital gain.
- **Mixing up "accrued interest paid" with "accrued market discount" (AMD).** They are different:
  - *Accrued interest paid:* Interest you prepay to the seller at purchase; subtracted from the first coupon. No IRS reporting.
  - *AMD:* Portion of the market discount you held the bond; reported by broker on 1099-B Box 1f at disposal; taxed as ordinary income.
- **Not tracking reopening auction accrued interest.** Your broker's notation is helpful but doesn't go to the IRS — you must copy it to Schedule B manually.
- **Entering 1099-B as a summary instead of one-by-one in TurboTax.** This prevents AMD from flowing to Schedule B and can trigger an IRS requirement to mail a paper statement.

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
