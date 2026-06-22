# MoU Review — Findings & Recommendations
**Document:** Memorandum of Understanding — Media Trust Limited × Alfalaq Technology Solutions Limited
**Project:** Media Trust Digital Platforms Revamp (22 weeks)
**Lens:** Neutral / balanced, perform-side aware · Governing law: Federal Republic of Nigeria
**Reviewer note:** Decision-support, not legal advice. Have a qualified Nigerian lawyer sign off before execution.
**On the proposal:** used as background only — *not* treated as authoritative. Where the MoU and proposal differ, the safer/more deliverable position is recommended, not the proposal's.

---

## 1. Executive Summary — the 5 biggest things we (Alfalaq) are committing to

1. **A 6-month warranty + 6-month support obligation (Cl. 14.3, 15.1) running from Final Acceptance — broader than the 90-day warranty we proposed, and priced into a contract value that isn't in the document.** We are on the hook to fix defects at no cost for half a year after a date we don't control. This is the single largest open-ended cost exposure in the MoU.

2. **A fixed 22-week, *sequential* timeline (Cl. 5.3) with almost no protection against client-caused delay.** If Media Trust is slow on approvals, access, content, or UAT, our schedule (and our committed team cost) slips with no contractual relief except force majeure. Meanwhile our payments are gated on *their* acceptance, with no deemed-acceptance backstop.

3. **Either party can walk on 30 days' notice (Cl. 18.1), and on exit we are only guaranteed payment for *completed and accepted* milestones plus non-cancellable costs (Cl. 18.3a).** Work done inside an unfinished milestone can go unpaid. Given the 30/30/25/15 milestone weighting, a termination mid-phase leaves a real cash gap.

4. **Cost responsibility for ongoing third-party services (Paystack fees, email, CDN/WAF, analytics) is not cleanly allocated.** Hosting is on Media Trust (Cl. 4.4), but recurring service fees sit in an ambiguous zone. Anything not clearly excluded can be argued onto us.

5. **The commercial core is missing or undefined.** Clause 8 (Payment) is blank, the liability cap (Cl. 16.1) and termination payments reference an undefined contract value, "adequate" insurance (Cl. 16.4) has no limits, and several operative terms ("Final Acceptance", "Business Days", "Working Hours", "Defect") are used but never defined.

---

## 2. Findings Table

| # | Clause | Issue type | Severity | Who it hurts | Finding | Recommended fix |
|---|--------|-----------|----------|--------------|---------|-----------------|
| 1 | 8 | Missing | Critical | Both | Payment Terms clause is entirely blank — no value, schedule, currency, tax, invoicing, interest. | Insert full payment terms (value, milestones, currency=NGN, VAT/WHT treatment, invoicing, deemed acceptance, late-payment interest). |
| 2 | 14.3 / 15.1 | Risk | High | Alfalaq | 6-month warranty + 6-month support from Final Acceptance — open-ended, exceeds proposal's 90-day warranty, ties to a date we don't fully control. | Confirm this is what was priced; cap free-fix scope to defects against spec, exclude data/content/3rd-party causes (partly in 15.4), and fix the warranty start trigger to a defined "Final Acceptance" or go-live date. |
| 3 | 5.1–5.3 | Risk | High | Alfalaq | Fixed 22-week *sequential* timeline; scope is large (PWA, CMS, paywall, AI, migration, security). Realism risk; "sequential" is stricter than how the work actually overlaps. | Add explicit assumptions/dependencies; allow phase overlap; add a time-extension (EOT) mechanism. |
| 4 | (missing) | Missing | High | Alfalaq | No **client-delay relief**. If Media Trust is late (approvals, access, content, UAT), only force majeure (Cl. 17) gives relief — which doesn't cover client delay. | Add a "Client Dependencies & Delay" clause: time + cost relief and milestone-date adjustment for documented client delay. |
| 5 | 9 | Loophole | High | Alfalaq | Acceptance needs Media Trust to act, but there is **no deemed-acceptance** time-bar. Payment can stall indefinitely. | Add: if no written acceptance/rejection within N business days of submission, the deliverable is deemed accepted. |
| 6 | 18.1 / 18.3 | Risk | High | Alfalaq | Termination for convenience on 30 days; on exit we get paid only for *completed & accepted* milestones + non-cancellable costs — partial-milestone work-in-progress may go unpaid. | Add payment for WIP up to termination on a pro-rata/time-and-materials basis, plus demobilisation costs; consider longer notice or a kill-fee. |
| 7 | 4.3 / 4.4 | Risk / Missing | High | Alfalaq | Ongoing third-party service costs not cleanly allocated. Hosting is Media Trust's (4.4), but Paystack fees, email/newsletter, CDN/WAF, analytics aren't named. Anything not excluded can be pushed onto us. | Add a "Costs & Charges" schedule listing every cost item and the responsible party (see §3). |
| 8 | 16.1 | Defect | High | Both | Liability cap = "total amount paid or payable" — but that amount is undefined (Cl. 8 blank). Cap is currently meaningless. | Define the cap by reference to the stated contract value once Cl. 8 is completed. |
| 9 | 16.4 | Loophole | Medium | Alfalaq/Both | "Adequate" PI + cyber insurance — no monetary limits, so "adequate" is unenforceable / open to dispute. | State specific cover amounts (e.g., PI ₦X, cyber ₦Y) and the period. |
| 10 | 11.5 | Loophole | Medium | Both | Source-code escrow only "to be negotiated within 30 days" if proprietary frameworks are used — an agreement to agree, unenforceable. | Either commit to escrow terms now (or a template schedule) or delete and rely on the perpetual licence in 11.2. |
| 11 | 11.1 / 11.2 | Risk | Medium | Alfalaq | IP in custom work transfers on full payment (good); pre-existing IP retained with a perpetual licence (good). Ensure "custom-developed *specifically for this Project*" is tightly worded so our reusable components/frameworks aren't swept into the transfer. | Tighten the definition boundary between custom deliverables and pre-existing/reusable IP. |
| 12 | 13.6 vs 4.4 | Loophole | Medium | Both | Cross-border data transfer banned without consent, but Cl. 4.4 allows AWS/Azure (regions often outside Nigeria). Potential built-in contradiction. | Require Nigeria-region hosting OR pre-authorise the chosen provider/region with NDPA transfer safeguards. |
| 13 | A (SLA) | Missing | Medium | Media Trust | 99.5% uptime target with **no remedy/service credit** if missed, and uptime depends on client-owned infra (4.4). | Add a service-credit/remedy mechanism, and carve out downtime attributable to client-owned infrastructure. |
| 14 | 12.3 | Conflict | Low | Both | Confidentiality survives 5 years; proposal said 2. 5 years is the safer, more standard position — keep it, just note the divergence is intentional. | Keep 5 years; no change needed beyond awareness. |
| 15 | 20.12 | Defect | Medium | Both | Survival list omits Clause 8 (payment) and Clause 15 (support) — accrued payment obligations should survive. | Add Clauses 8 and 15 (or the payment-survival point) to the survival list. |
| 16 | 13.4–13.5 / Sch D §7–8 | Remove/Consolidate | Low | Both | Breach-notice and return/deletion terms restated verbatim in the DPA. | Replace Schedule D §7–8 with a cross-reference to Cl. 13.4–13.5. |
| 17 | 14.3 / 15.1 | Remove/Consolidate | Low | Both | Warranty and support both run "6 months from Final Acceptance" — overlapping and potentially confusing. | Clarify the relationship (warranty *within* the support period, or distinct scopes) to avoid double-counting. |
| 18 | 5.4 / 6 / 10.4 | Defect | Medium | Both | Leftover editing notes "New cluase" / "New clause" left in the body. | Delete all stray editorial artifacts. |
| 19 | 20.9 | Defect | Medium | Both | Notices clause has `[Insert Registered Address / Email / Name]` placeholders; both parties' emails blank. | Fill in full notice details for both parties. |
| 20 | Sch C | Defect | Medium | Both | Key Personnel "Qualification" column blank for all three named persons; titles differ from the proposal team list. | Complete qualifications; reconcile titles. |
| 21 | Effective Date | Defect | Medium | Both | Effective Date "25 June 2025" pre-dates the engagement (proposal Mar 2026) — almost certainly a typo. | Correct the year; align with actual execution date; date the signature blocks. |
| 22 | 21 / Sch C | Risk | High | Both | Alfalaq signs via "Project Manager / Authorized Representative" (Dr. Bashir Sani). A PM may not have authority to bind the company. | Sign through a director/MD (consistent with the proposal's "Managing Director"); ensure board authority + company stamp. |
| 23 | 1.1 | Missing | Medium | Both | Defined terms used but not defined: "Business Days", "Working Hours", "Final Acceptance", "Defect", "Commencement Date", "Requirements Specification". | Add definitions; "Final Acceptance" in particular drives warranty/support start. |
| 24 | 10.3 | Conflict | Low | Both | Change-request payment due in 14 business days, but milestone payments (per proposal) within 5. Inconsistent payment rhythm. | Align change-order payment timing with the main payment terms. |
| 25 | Sch D §3 | Conflict | Low | Both | DPA specifies TLS 1.2+; proposal/architecture says TLS 1.3. | Align to TLS 1.3 (the stronger, stated standard). |
| 26 | 4.2.7 | Conflict | Low | Both | Post-go-live stabilisation "minimum 14 days" sits alongside a separate 6-month support period — relationship unclear. | Clarify the 14-day intensive stabilisation vs. the 6-month support window. |

---

## 3. Cost-Responsibility Matrix

| Cost item | Should bear | Where MoU says so | Status / action |
|-----------|-------------|-------------------|-----------------|
| Cloud hosting — production/staging/DR (setup + recurring) | Media Trust | Cl. 4.4; Cl. 4.3 (recurring excluded) | ✅ Clear — keep. |
| Hardware / servers / devices | Media Trust | Cl. 4.3 | ✅ Clear. |
| Third-party software licences | Media Trust unless in pricing | Cl. 4.3 ("except where expressly included in the pricing") | ⚠️ Ambiguous — pricing (Cl. 8) is blank; specify which licences, if any, are inside scope. |
| Paystack transaction fees (1.5% + ₦100) | Media Trust | **Not stated** | ❌ Gap — add explicitly (proposal excludes them; MoU is silent). |
| Email/newsletter platform fees | Media Trust | Arguably under 4.3 "recurring infrastructure" | ⚠️ Not named — make explicit. |
| CDN / WAF (e.g., Cloudflare) recurring | Media Trust | Arguably under 4.3 | ⚠️ Not named — make explicit. |
| Analytics/BI tooling subscriptions | Media Trust | Arguably under 4.3 | ⚠️ Not named — make explicit. |
| Professional indemnity + cyber insurance | Alfalaq | Cl. 16.4 | ⚠️ Named but no limit amounts. |
| Source-code escrow agent fees | Unallocated | Cl. 11.5 (escrow undecided) | ❌ Gap if escrow proceeds — state who pays. |
| Cost overruns from client delay | Should be Media Trust | **Not stated** | ❌ Gap — tie to new client-delay clause (Finding #4). |
| Data return/deletion on exit | Likely Alfalaq | Cl. 13.5 (no cost stated) | ⚠️ Clarify whether at Alfalaq's cost. |
| New development after Final Acceptance | Media Trust (via Change Request) | Cl. 4.3, Cl. 10 | ✅ Clear. |

**Recommendation:** add a single **Schedule E — Costs & Charges** that lists every row above with the responsible party, so nothing recurring can later be argued onto Alfalaq.

---

## 4. Missing Clauses to Add (with suggested drafting)

- **Payment Terms (fill Cl. 8).** *"The total contract value is NGN [____] (inclusive of VAT at 7.5%). Payment shall be made in Nigerian Naira against the milestones in Schedule [__], each invoice due within [5] Business Days of written Acceptance (or deemed Acceptance) of the corresponding Deliverable. Withholding tax shall be handled per applicable Nigerian law. Late payments accrue interest at [__]% per month."*
- **Client Dependencies & Delay.** *"Where MEDIA TRUST fails to provide access, approvals, content, or UAT within the agreed periods, ALFALAQ shall be entitled to a day-for-day extension of affected milestone dates and recovery of reasonable standby/re-mobilisation costs, and shall not be in breach for resulting delay."*
- **Deemed Acceptance (amend Cl. 9).** *"If MEDIA TRUST does not issue a written acceptance or a reasoned rejection within [10] Business Days of submission of a Deliverable, that Deliverable shall be deemed accepted."*
- **Costs & Charges (Schedule E).** Per §3 above.
- **Termination payment for WIP (amend Cl. 18.3).** *"…plus payment, on a pro-rata basis, for work performed within any milestone not yet completed as at the termination date, together with reasonable demobilisation costs."*
- **Insurance limits (amend Cl. 16.4).** State specific PI and cyber cover amounts and the period maintained.
- **SLA remedy (Schedule A).** Service credits or a cure mechanism for uptime/SLA breaches, excluding client-infrastructure-caused downtime.
- **Definitions (Cl. 1.1).** Add "Business Days", "Working Hours", "Final Acceptance", "Defect", "Commencement Date", "Requirements Specification".

---

## 5. Remove / Consolidate

- **Delete** all leftover editing notes: "New cluase" (after Cl. 5.4 and before Cl. 6) and "New clause" (Cl. 10.4).
- **Consolidate** Schedule D §7–8 into a cross-reference to Cl. 13.4–13.5 (currently verbatim duplication).
- **Clarify/merge** the warranty (Cl. 14.3) and support (Cl. 15.1) periods so the two 6-month obligations aren't read as conflicting or double-counted.
- **Resolve** the escrow placeholder (Cl. 11.5) — commit terms now or delete the agreement-to-agree.

---

## 6. Pre-Signature Checklist (ordered by how badly it hurts us if left as-is)

1. ☐ **Complete Clause 8 (Payment)** — value, milestones, currency, VAT/WHT, invoicing, interest; and update the liability cap (16.1) to reference it.
2. ☐ **Add client-delay relief + deemed acceptance** (Findings #4, #5) — protects our schedule and cash flow.
3. ☐ **Fix the termination-for-convenience payout** to cover work-in-progress + demobilisation (Finding #6).
4. ☐ **Confirm the 6-month warranty/support is what we priced**, define its start trigger ("Final Acceptance"), and bound the free-fix scope (Finding #2).
5. ☐ **Add the Costs & Charges schedule** so recurring third-party/hosting costs can't fall on us (Finding #7, §3).
6. ☐ **Set insurance limits** (Finding #9) and **resolve escrow** (Finding #10).
7. ☐ **Sign through a director/MD with company authority + stamp** (Finding #22).
8. ☐ **Resolve the data-residency contradiction** (13.6 vs 4.4) (Finding #12).
9. ☐ **Add an SLA remedy** and carve out client-infra downtime (Finding #13).
10. ☐ **Clean drafting defects**: remove "New cluase"/"New clause"; fill Notices placeholders; complete Schedule C qualifications; correct the Effective Date year; date the signatures; add missing definitions; fix survival list (Findings #15, #18–#21, #23).
