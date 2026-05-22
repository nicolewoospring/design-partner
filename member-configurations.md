# Member configurations

Spring Health–specific dimensions that change member experience. **When brainstorming, ask which dimensions apply to the project, then propose prototype variants that cover the meaningful combinations.**

For any project touching payment, insurance, cost estimates, or billing, **start with cohort** — it's the single highest-leverage dimension and gates a lot of downstream behavior.

---

## Cohort (primary dimension)

Cohort is determined by customer contract setup. It dictates whether the cost estimate tool runs at all, whether insurance can be added, and what the "Costs and coverage" tab shows.

### 1. Excluded
- Excluded from the cost estimate tool (rate card issues, unique customer contracts).
- **Never sees the "Costs and coverage" tab.**
- Every cost-estimate CTA terminates in a `Cost estimate has been requested` confirmation screen and auto-creates a Zendesk ticket.
- Whether they have insurance or not is irrelevant — the tool doesn't run for them.

### 2. Insurance ineligible
- No CSN, not within a Payer customer.
- **The platform has zero insurance inputs for this cohort.** No insurance form. No "Add insurance" affordances. By design.
- "Costs and coverage" tab is visible and shows the self-pay rate without a health plan details section.
- **Care Support comms must not suggest adding insurance** to this cohort — it inspires false hope. Any prototype touching this cohort needs to be checked for accidental insurance prompts.

### 3. CSN (insurance-eligible)
- Has a CSN. Eligible to add insurance, but hasn't necessarily done so.
- Greatest variation in flows. The member's experience further branches on:
  - **Payment preference** (not declared / insurance / self-pay) — gates whether the Costs & coverage tab appears at all
  - **Insurance validation status** (auto-validated / pending manual validation / manually validated)
- Sub-state matrix below.

### 4. Payer (insurance sign-up)
- Within a Payer customer. Member access to Spring *is* through insurance, so insurance is on file from day one.
- Cost estimate CTAs skip the cost estimate flow entirely — they go straight to "Costs and coverage."
- Same auto/manual validation branches as CSN.

---

## Sub-states within cohorts 3 and 4

### Payment preference (CSN only)
For CSN members, until they declare a payment preference, the **Costs and coverage tab is hidden**. Declaration happens inside the cost estimate flow.

- **Not declared** — default state. Costs & coverage tab hidden.
- **Insurance** — member chose to add insurance and proceeded through the form.
- **Self-pay** — member explicitly chose self-pay.

### Insurance validation status
Applies to anyone with insurance on file (CSN + Payer cohorts):

- **None on file**
- **Auto-validated** — instant eligibility check passed. Green checkmark, plan name + group ID auto-fill.
- **Pending manual validation** — additional fields required (plan name, group ID, card photos). Submission auto-creates a Zendesk ticket; member is told to check email.
- **Manually validated** — completed manual review. (Note from the doc: not visible in Admin.)

---

## "Costs and coverage" tab visibility matrix

| Cohort | Sub-state | Tab visible? | What it shows |
|---|---|---|---|
| Excluded | — | Never | — |
| Insurance ineligible | — | Yes | Self-pay rate. No health plan details section. |
| CSN | No preference declared | Hidden | — |
| CSN | Self-pay declared | Yes | Self-pay rate + banner inviting them to add insurance if they change their mind |
| CSN | Insurance auto-validated | Yes | Insurance estimate ($X from you / $Y covered) + health plan progress (deductible, OOP max, 100% covered) |
| CSN | Insurance pending manual validation | Yes | Full rate + banner directing them to check email for custom estimate |
| Payer | Auto-validated | Yes | Same as CSN auto-validated |
| Payer | Pending manual validation | Yes | Same as CSN manual validation |

---

## Other dimensions (orthogonal to cohort)

### Persona
`member`, `provider`, `care-navigator`, `medication-manager`, `coach`, `hr-leader`. Most member-facing prototypes target `member`. Each non-member persona has a different surface (Spring Care vs Spring Practice vs Spring Insights).

### Geography
- **US member** — default; full feature set, USD pricing, US-licensed providers.
- **Global member** — international; may not be eligible for insurance, different licensing pool, currency considerations, timezone implications.

### Sponsored session balance
- **Has unused sponsored sessions** — can book at no cost up to bundle limit. Cost estimates for future non-sponsored sessions are visible alongside the no-cost current sessions, so the member can preview what comes after their bundle.
- **Exhausted** — bundle used up, all future sessions are at-cost.

### Account billing state
- **Active / good standing** — no payment issues.
- **Grace period** — outstanding balance, can still book within window.
- **Scheduling block** — outstanding balance past grace, cannot book new sessions.

### Tenure
- **New** — just signed up, hasn't completed first session.
- **Active** — engaged, has provider relationships.
- **Returning / lapsed** — was active, now re-engaging.
- **Long-time** — multi-year, has substantial care history.

### Provider relationship
- **No provider yet** — pre-matching.
- **Has 1 provider** — single therapy or medication relationship.
- **Has multiple providers** — therapy + medication, therapy + coaching, etc.
- **Provider unavailable** — on leave, left network, not accepting new patients.

### Active care modalities
- Therapy only / Medication only / Therapy + medication / Coaching / Self-guided / Moments only.

---

## Cost estimate tool — known coverage gaps

The tool currently does **not** support cost estimates for:

- Therapy in-person / couples (CPT `90837`)
- Medication management in-person (CPT `99212`)
- Coaching (any modality)
- Specialty care (another pod, TBD)

Tool accuracy is ~85%. Incorrect estimates are somewhat expected; the team files support cases with **Apero** when wrong estimates surface.

---

## Combinations worth flagging

Some intersections create meaningfully different design problems. Add notable ones here as you encounter them.

- **Excluded cohort + any cost touchpoint** — the only valid outcome is "request a cost estimate" → confirmation screen + Zendesk ticket. Don't show price UI.
- **Insurance ineligible + any cost touchpoint** — must avoid suggesting insurance. Self-pay-only language, no insurance form.
- **CSN + payment preference not declared** — Costs & coverage tab is hidden. Designs that link to this tab from elsewhere (e.g. appointment confirmation) need a fallback for these members.
- **CSN + manual validation pending** — member sees full rate temporarily and is told a custom estimate is coming via email. Be careful not to let this read as the "final answer."
- **Global + post-bundle + self-pay** — currency display becomes critical (see `global-member-pay` project).
- **Active care modality is coaching / in-person therapy / specialty care** — cost estimate tool can't price it. Plan an alternate path.

---

## How to use this when brainstorming

For each prototype idea:

1. **Cohort first.** Which of the 4 cohorts does this design need to support? If it touches cost, payment, or insurance, all four likely need consideration.
2. **For CSN, layer in sub-state.** Payment preference + validation status produce 5 meaningfully different "Costs and coverage" experiences. Pick the 2–3 that most stress-test the design.
3. **Are there orthogonal dimensions** (geography, sponsored balance, billing state) that meaningfully change the layout or copy?
4. **Is the prototype touching a service type the tool can't price?** If so, the variant should show the alternate path, not a fake estimate.

Build the meaningful sub-states as togglable variants in the prototype so the team can flip through them in one place.
