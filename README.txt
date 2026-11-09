THE 1099 RADAR — free giveaway from "Build It With AI", Episode 25
===================================================================

WHAT IT IS
A Google Sheets + Apps Script tool. Paste your year's payment ledger and vendor list in, click
"1099 Radar → Build the report", and it tells you: which vendors need a 1099-NEC, which rent needs
a 1099-MISC, which W-9s you are missing (and what that exposure costs), which payments are the
card processor's job rather than yours, what it refused to read and why, and a to-the-cent
self-audit that refuses to vouch for a report that does not tie.

It FILES NOTHING and SENDS NOTHING. And it is not a tax professional: it sorts YOUR ledger by the
IRS's published rules (sources below) so the conversation with your accountant is short. Odd cases
— medical payments, attorney gross proceeds, royalties, backup withholding you actually owe — are
exactly what that conversation is for.

SET-UP (about 3 minutes)
1. Make a Google Sheet with tabs named: Vendors, Payments (optionally Settings).
   Vendors:  Vendor | Entity type | W-9 on file | Email
   Payments: Date (YYYY-MM-DD) | Vendor | Description | Category | Method | Amount
   Category: Services, Legal services, Parts & materials, Rent, Goods only
   Method:   Check, ACH, Zelle, Cash, Wire  (yours to report)
             Credit card, Debit card, PayPal, Venmo, Square  (processor reports on 1099-K)
2. Extensions → Apps Script → paste radar.gs → save → reload the sheet.
3. "1099 Radar" menu → Build the report. Try the sample CSVs in this bundle first.

SETTINGS tab (optional, two columns: Setting | Value)
  threshold    2000          (the TY2026 law; set 600 to see the retired rule)
  taxYear      2026
  penaltyTier  after-aug-1   (or by-aug-1, 30-days — prices the exposure card)
  dupDays      3             (exact-duplicate window; 0 disables)

FILES
  radar.gs                                the tool (prompt 3's build — the only one to run)
  radar_v1_FIRST_BUILD_NOT_THE_TOOL.gs    NOT THE TOOL — the $600-threshold wreck, kept for study
  radar_v2_SECOND_BUILD_NOT_THE_TOOL.gs   NOT THE TOOL — exempts the law firm, drops Zelle & parts
  checker.py                              the independent Python second opinion from the episode
  SPEC.md                                 the exact rules both implementations follow
  vendors.csv, payments.csv               Saltmarsh Pottery Works, the fictional sample business
  PROMPTS.txt                             the three prompts exactly as sent

SOURCES (read 2026-11-07/08 — reread them before you file; rules and amounts move)
· Threshold $2,000 for tax years beginning after 2025; corporations exempt EXCEPT legal services;
  card/third-party-network payments go on the processor's 1099-K; rent ≥ $2,000 on 1099-MISC box 1;
  NEC box 1a includes parts and materials:
  https://www.irs.gov/instructions/i1099mec  (12/2026 revision)
· Penalties, returns due 2027: $60 / $130 / $340 per form by lateness, $690 intentional disregard,
  charged separately for the information return and the payee statement:
  https://www.irs.gov/payments/information-return-penalties  (page updated 30-Oct-2026)
· Backup withholding, 24%: https://www.irs.gov/businesses/small-businesses-self-employed/backup-withholding
· Track1099 by Avalara pricing (the paid comparison in the episode): $3.10/form first 15 federal
  e-files, $1.49/form state, $2.89/mailing Jan 27–31:
  https://www.avalara.com/us/en/products/1099/pricing.html  (page modified 2026-10-15)

VERIFICATION SHIPPED WITH THIS EPISODE
209 paired runs (frozen fixture × 9 settings + 200 generated businesses) against the independent
Python checker: 22,906 fields compared, 0 disagreements. 38 functional checks against a mock
Sheets runtime, including the DO-NOT-TRUST demo as a real failing run. Planted-fault proofs: the
law-firm exemption bug trips 1,873 disagreements; the Zelle bug trips 3,680.

Sample data is fictional (@example.com). No real business, person, or vendor is represented.
