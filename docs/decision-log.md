# Decision Log

A running record of significant decisions on this project: the options considered, the trade-offs, and what was chosen. New entries go at the bottom. Reversed decisions stay in the log, marked as reversed, not deleted.

---

## D1 — Narrow the brief to one specific use case

**Context:** The original brief ("AI decision reliability × AI decision overload") was too broad to validate or build as a solo student project in 4–6 weeks.

**Options considered** (full scoring in [Phase 01](phase-01-problem-validation.md)):
| Option | Main reason for/against |
|---|---|
| A. University/program shortlisting | Strong researchability, personal access to the user population, underserved evidence/trade-off angle |
| B. Job offer comparison | Less overlooked, a spreadsheet does most of the job |
| C. Expensive consumer purchases | Crowded market, low stakes |
| D. Evaluating AI-generated study material | Collapses toward "AI fact-checker," which the brief ruled out |
| E. Founder decisions | Hard to recruit real participants |

**Chosen:** A, narrowed further to funding-constrained graduate applicants abroad.

**Trade-off accepted:** a narrower audience in exchange for a segment that can realistically be interviewed in two weeks. The scores behind this ranking are my judgment, not measured data.

---

## D2 — Verdict: MODIFY, not build or abandon

**Context:** Phase 01 desk research found a real gap (evidence-first decision tools for consumers are rare; generic AI pros/cons apps are crowded) but also a finding that cuts against the original hypothesis (see Open Doubts).

**Options:** build as briefed/modify and narrow/abandon.

**Chosen:** modify. Revised problem statement is at the end of Phase 01.

**Trade-off accepted:** the project's scope is now defined by a hypothesis that has not been tested with real users.

---

## D3 — Design boundary: no admission-probability prediction

**Context:** Counsellor reports found in Phase 01 research describe AI inflating students' admission chances.

**Decision:** The product will not predict admission odds or name a "best" school. This is stated in the README.

**Reasoning (mine, not yet tested):** Building this feature would reproduce the failure mode the project exists to counter. It also can't be validated honestly with the data available to a solo student.

**Status:** draft boundary. It can be revisited if interviews show a strong need, but it needs evidence to change.

---

## D4 — Repo name: `gradledger`

**Options considered:**
- First round: `shortlist`, `evidence-ledger`, `gradshort` / `shortlist-evidence`, `decision-ledger`. `evidence-ledger` was recommended because it names the mechanism.
- After the request for a name tied to graduation and universities: `shortlisted`, `gradledger`, `applywise`, `unishortlist`.

**Chosen:** `gradledger`: domain (grad school) plus mechanism (evidence ledger) in one short word.

**Trade-off:** The name ties the project to the grad-applicant segment. If research moves the target user, the name may need to change.

---

## D5 — Validate with real interviews before writing any code

**Context:** Working rule: prove the problem is real before proposing a product.

**Decision:** No prototype until interviews have been run and logged. The plan, including a pre-set decision rule, is in [Phase 02](phase-02-user-research-plan.md).

**Note on the decision rule:** the "roughly one third of participants" threshold was chosen by the assistant as a reasonable starting point and was not derived from literature. It was set before any data exists, so it cannot be adjusted afterwards to fit results.

---

## D6 — Incremental, honest commits, pushed manually

**Decision:** each document is its own commit with a message describing what actually changed, pushed manually from VS Code, as in the FitMatch project.

---

## Open doubts

1. **The overload half of the hypothesis may be wrong.** Phase 01 cites a study in which people responded positively to large numbers of AI-generated options. If interviews show trust miscalibration without real overload, the project is about trust, not overload.
2. **Phase 01 figures and citations are unverified.** Statistics and study details in Phase 01 (including the survey percentage in the Phase 03 scoring section and the choice-overload study findings) came from web search results and have not been checked against primary sources. Treat them as unverified until a sources file confirms them.
3. **Phase 01 scores are judgments.** The 1–10 scores in the problem-space table are the assistant's estimates, not measurements.
4. **Sample bias.** Early interviews will likely come from the author's own network and online communities, which may not represent applicants generally.

---

## Process notes (mistakes worth recording)

- A nested `gradledger/gradledger` folder was created by accident while setting up the repo, and was removed before the first commit.
- The `.gitignore` contents were pasted into the terminal instead of a file. The terminal rejected them as commands and nothing was changed.
