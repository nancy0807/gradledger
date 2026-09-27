# Project 3 — Problem Validation (Phases 1–10)
**Working title of the brief:** "AI Decision Reliability × Decision Overload"
**Status:** Conceptual validation only. No code, no PRD, no build decisions yet — as instructed.

---

## PHASE 1 — Problem Discovery

You've bundled several distinct phenomena under "AI trust" and "decision overload." They need to be pulled apart before any product can be designed, because each one implies a different fix.

| Concept | What it actually is | Wrong fix if you treat it as something else |
|---|---|---|
| **Factual accuracy** | Is the AI's claim true? | A confidence score doesn't fix a wrong fact. |
| **Calibration** | Does the AI's *stated* confidence match its *actual* hit rate? | This is the technical core of "trust" — and it's a solved-ish ML problem (temperature scaling, verbalized confidence), not a UX problem alone. |
| **Explainability** | Can a human see *why* the AI said what it said? | Explaining a wrong answer clearly just makes people trust the wrong answer more (documented — see Phase 2). |
| **Automation bias** | Humans over-trusting AI output because it's AI, independent of accuracy | Adding more explanation can *worsen* this if the explanation reads as authoritative. |
| **Algorithm aversion** | Humans under-trusting AI even when it's more accurate than they are, especially after seeing it err once | The opposite failure mode — also real, also documented. |
| **Choice overload** | Too many options degrades decision quality/satisfaction, independent of whether the options came from AI | Classical behavioral-econ finding (Iyengar & Lepper's jam study; Schwartz's "paradox of choice"). |
| **Decision compression** | The active process of turning N options into a defensible shortlist without losing the reasoning | Not the same as "showing fewer options" — a badly compressed shortlist is worse than a well-organized long list. |
| **Cognitive load** | The working-memory cost of processing information, regardless of how many discrete "options" exist | You can have 3 options and huge cognitive load if the trade-offs are entangled. |

**Is this a new problem or an old problem with a new interface?**
Mostly the latter, with one genuinely new element. Choice overload (Iyengar & Lepper 2000), automation bias (Skitka et al. 1999), and algorithm aversion (Dietvorst et al. 2015) all predate LLMs by decades. What's new is **generation speed and fluency**: pre-LLM, producing 20 well-written, confident-sounding, personalized options for a stranger took a human expert hours. Now it takes seconds and it's free. The bottleneck used to be *option generation*; it's now entirely shifted to *option evaluation*. Humans haven't gotten faster at evaluating — so the bottleneck moved to a stage we have no tools for. That's the real "new" problem: **supply of plausible-sounding options has decoupled from supply of judgment**, and the interfaces (chat windows) that generate the options offer almost nothing to help with the evaluation stage.

**What happens today, without a product like this:**
- People either stop at the first AI answer (automation bias / satisficing), or
- They re-prompt the AI over and over trying to manufacture their own confidence ("are you sure?", "double check this"), which doesn't add real evidence, or
- They open 10 browser tabs to manually cross-check, which defeats the point of asking AI at all, or
- They ask a second AI, then a human, then give up and go with gut feeling anyway.

**Who experiences this, specifically:** anyone using AI for a decision that (a) has real stakes, (b) has no single correct answer, and (c) they can't fully verify themselves in the time they have. That's a huge population — but "huge population, vague problem" is exactly the trap Phase 4 exists to avoid.

---

## PHASE 2 — Existing Landscape (researched, not assumed)

### Academic / research grounding — this is a real, active research area, not a fringe idea
- **Evaluative AI (Miller, 2023, FAccT)** argues that recommendation-first AI is inherently persuasive rather than evidential — it justifies its own answer instead of showing evidence for *and against* every option. His proposed alternative — surfacing evidence for/against each option without picking a winner — is close to your instinct, and it's a named academic framework you should read and cite, not reinvent from scratch.
- **"Not All Uncertainty Is Equal" (2026)** studies how the *granularity* of stated uncertainty (a single number vs. broken-down-by-source uncertainty) changes whether humans actually verify AI claims. Coarse confidence scores barely change verification behavior; granular, source-attributed uncertainty does more.
- **Verbalized uncertainty research (Xiong et al. 2023; Xu et al. 2025)** shows LLMs *can* express calibrated-ish uncertainty in words, but naive confidence scores are often poorly calibrated and can mislead more than they help if presented as precise numbers.
- **Choice overload + AI, specifically (Kim et al., Journal of Retailing and Consumer Services, 2023)** is the finding you most need to know, because it complicates your core hypothesis: across five studies, people responded *positively* to large numbers of AI-generated recommendations (up to 60), more than they would to the same volume from a human — likely because AI recommendations read as more personalized/effortless to sift. **This means "AI gives too many options → overload" is not a clean, proven effect.** Classical choice-overload research (Schwartz; six options outperforming thirty in some studies) still holds for *human-curated* choice sets. Your product can't just assert "AI causes overload" — it needs to test whether overload shows up specifically in *high-stakes, hard-to-verify* decisions (career, university, health, big purchases) versus the low-stakes ones (songs, restaurants) these studies used.
- **Automation bias / algorithm aversion literature** (Skitka et al.; Dietvorst et al.; Prahl & Van Swol) gives you the two failure modes to design against: over-reliance and under-reliance. A good product has to move the *calibration*, not just push people toward "less trust" or "more trust" uniformly.

### Existing products — and why none of them are your product
- **Decido, "Decision Journal – Pros & Cons," "Choices AI," "Decision AI"** (all live apps, 2026): every one of these is a pros/cons-weighting wrapper around an LLM call. Enter a decision → AI gives pros/cons or a weighted score → verdict. **This is the generic wrapper you were explicitly told not to build**, and it already exists, several times over, on both app stores. None of them do evidence sourcing, none show uncertainty as a first-class object, none do option compression from a large AI-generated set — they all assume you already narrowed things down to 2–3 named options.
- **Perplexity / Copilot-style "AI answer engines"** show citations, which is a step toward evidence, but they don't do trade-off structuring, don't quantify uncertainty, and don't compress a large option space — they answer one question at a time.
- **Recommendation/decision-support systems in the enterprise/consulting space** (Deloitte's "AI as trusted advisor" framing, industrial "AI trust" papers) are real but aimed at executives and operational systems, not individual consumer decisions — different user, different stakes, different interface needs.
- **RAG-based / knowledge-graph decision systems** (e.g., academic work on startup evaluation) show the "evidence + reasoning + human override" pattern is technically real and buildable at small scale, which is useful precedent for your architecture in Phase 6 — but they're built for domain experts, not first-time individual decision-makers.

**Conclusion of Phase 2:** the "AI decision helper" wrapper space is already saturated and low-quality. The "evidence-and-uncertainty-first, non-persuasive" approach (Evaluative AI) is validated in research but has almost no consumer-facing product built around it. **That gap — a consumer decision tool built on evidential/option-awareness principles instead of a single recommendation — is real and mostly unoccupied.** But "evidence-first decision tool" is still too broad to build in 4–6 weeks; Phase 3 and 4 exist to narrow it into something a solo student can actually validate.

---

## PHASE 3 — Overlooked Problem Spaces (scored)

Scoring 1–10 each on: **Sev**erity, **Freq**uency, **Over**lookedness, **AI-Nec**essity, **Feas**ibility (solo, 4–6wk), **Res**earchability (can you get 10–20 interviews), **Meas**urability, **Orig**inality, **PM-port**folio value, **Strat-port**folio value.

### A. Students building a university/program shortlist with AI
- **Problem:** Students feed AI their profile and get a "college list" — but multiple counselors report AI produces near-identical lists across different students, over-inflates admission chances (sycophancy), and gives no way to see *why* a school is ranked where it is or *how confident* that ranking should be. A 2026 counseling-industry survey found 61% of students felt overwhelmed by the advice they'd collected, AI included.
- **Target user:** high-school seniors / master's applicants building a shortlist from 100+ possible schools down to 8–15 real applications.
- **Current behavior:** ask ChatGPT for "best universities for X," get a generic top-10 list, cross-check nothing, apply broadly out of anxiety, or trust AI's optimism about admit chances.
- **Why existing solutions fail:** ChatGPT has no memory of *this student's actual constraints* (funding, visa, deadlines) unless manually re-fed every time; college-search sites (Niche, official rankings) have filters but no reasoning or trade-off view; human counselors are expensive and slow.
- **Why overlooked:** everyone treats this as a "search/filter" UX problem (more filters!) rather than an *evidence + uncertainty + trade-off compression* problem.
- **AI role:** aggregate scattered evidence (scholarship terms, visa/OPT-equivalent rules, historical admit data, program specifics) with source attribution and explicit "we don't know this" flags; compress from "all possible schools" to a defensible shortlist with visible trade-offs.
- Scores: Sev 8, Freq 6, Over 6, AI-Nec 7, Feas 6, Res 9 (you can literally recruit from your own applicant cohort), Meas 6, Orig 6, PM-port 7, Strat-port 6.

### B. Job seekers evaluating multiple offers/roles with AI-generated comparisons
- **Problem:** People ask AI to compare offers/companies; AI is fluent but has no real evidence about the specific team, manager, or role — comparisons look rigorous but are often just plausible-sounding text.
- Scores: Sev 7, Freq 6, Over 4 (fairly well covered by career-coaching content), AI-Nec 5, Feas 5, Res 6, Meas 5, Orig 4, PM-port 5, Strat-port 4. **Weaker: less overlooked, weaker AI-necessity (a spreadsheet mostly does this job).**

### C. Consumers making one expensive, infrequent purchase (e.g., laptop, appliance) with AI recommendations
- **Problem:** AI "best X for Y" content is often SEO-poisoned or affiliate-driven; users can't tell evidence from marketing.
- Scores: Sev 4, Freq 8, Over 3 (very crowded — Wirecutter, Rtings, countless AI shopping tools), AI-Nec 4, Feas 6, Res 7, Meas 6, Orig 3, PM-port 4, Strat-port 3. **Weak: low stakes, extremely crowded, hard to differentiate.**

### D. Students evaluating AI-generated study/research material for accuracy before using it academically
- **Problem:** Students use AI to summarize papers/generate study notes and can't tell what's solid vs. hallucinated, especially under academic-integrity pressure.
- Scores: Sev 6, Freq 7, Over 5, AI-Nec 7, Feas 5, Res 7, Meas 5, Orig 5, PM-port 5, Strat-port 5. **Reasonable but adjacent to "AI fact-checker," which you were told to avoid; hard to keep it from collapsing into that.**

### E. Founders/solo builders evaluating early business/product decisions using AI
- **Problem:** Solo founders use AI to validate ideas, market size, pricing — AI tends to be encouraging regardless of merit (same sycophancy issue as college advice).
- Scores: Sev 6, Freq 4, Over 6, AI-Nec 6, Feas 5, Res 5 (hard to recruit real founders at volume), Meas 4, Orig 6, PM-port 6, Strat-port 6. **Interesting but weak on researchability for a student.**

**Ranking by combined score and, more importantly, by what you can actually pull off in 4–6 weeks with real interviews: A (university/program shortlisting) is the strongest candidate.** It also happens to be the one space where you are *currently* the user — you are, right now, running a 15-university shortlist through a Notion HQ for your own Master's applications. That's not a coincidence to ignore; it's a massive research-access advantage most classmates won't have.

---

## PHASE 4 — Choosing a Specific Use Case

**Recommended narrow segment:** *Master's/graduate-program applicants (India-based, applying abroad, funding-constrained) building and defending a shortlist of universities/programs under deadline and scholarship pressure.*

This is narrower than "students choosing universities" in three important ways:
1. **Funding-constrained** — scholarship viability is a hard filter most college-search tools don't model well, and it's exactly the kind of "evidence that's scattered across scholarship pages, forums, and outdated blog posts" problem AI is good at aggregating *if* it shows its sourcing.
2. **Graduate-level, not undergrad** — undergrad college-list tools (Niche, admissions consultants) are a much more saturated market; grad-school shortlisting is thinner.
3. **India-abroad specifically** — a definable, reachable interview population (your own cohort, LinkedIn, Discord/Reddit communities like r/gradadmissions), with genuinely different constraints (visa rules, cost-of-living, currency) than the U.S.-domestic college-search tools were built for.

You can realistically interview 10–20 people in this segment inside two weeks without paying for recruitment.

---

## PHASE 5 — Product Concept (draft, pending interview validation)

- **Working name:** *gradledger* (evidence-ledger mechanism, grad-school domain)
- **One-line value prop (draft):** Turns "AI gave me 40 plausible universities" into a shortlist you can actually defend — with the evidence, the gaps, and the trade-offs visible, not hidden inside a chat transcript.
- **Target user:** graduate applicants abroad, funding-constrained, applying to 10+ programs in parallel.
- **Trigger moment:** the point where a student has an AI-generated or self-researched list of 20–50 "possible" programs and needs to cut it to a defensible 8–15 to actually apply to.
- **Current workflow:** ask ChatGPT repeatedly, copy answers into a spreadsheet/Notion manually, lose track of *why* each school was included, re-ask the same questions in new chats and get inconsistent answers.
- **New workflow:** input constraints once (budget, field, target intake, must-haves) → system pulls candidate programs → for each, shows evidence *and its source*, explicit unknowns/unverified flags, and a trade-off view against the student's stated priorities → student actively cuts/keeps with reasoning recorded → system tracks confidence in the remaining shortlist and flags where more research is still needed before deadlines.
- **What the AI does:** aggregates and structures publicly available program/funding info with source links; flags what's unverified/unverifiable; generates trade-off comparisons across the student's *own stated criteria* (not a generic ranking).
- **What the AI explicitly does NOT do:** predict admission probability (this is exactly the sycophancy failure mode from Phase 3 research — do not rebuild it), pick a "best" school, or replace official sources.
- **Human-in-the-loop mechanism:** every removal/keep decision requires the student to state a reason; the system never auto-removes a school.
- **Evidence interface:** every claim shows a source and a "last verified" state; unverifiable claims are visually distinct, always, everywhere — matching your own working rule about unverified data.
- **Uncertainty interface:** per-criterion, not a single blended score (the "granular uncertainty" finding from Phase 2 — single scores don't change behavior, source-level uncertainty does).
- **Decision compression mechanism:** side-by-side trade-off view limited to a small number of programs at a time (informed by the 6-ish "Goldilocks" range from choice-overload literature), with an explicit "why this one is out" log the student can revisit.
- **Failure modes to design against:** AI over-stating confidence in scraped funding info (real money at stake if wrong); the tool becoming just another thing to over-trust (must design against automation bias, not just choice overload); stale data (scholarship terms change yearly).
- **Safety / privacy:** no scraping/storing personal application essays or ID docs; funding and admission data only from public sources with links, never invented.
- **North Star metric (draft, needs interview validation):** % of shortlist decisions where the student can state, unprompted, the evidence and trade-off behind why a school is in/out — a proxy for "decision was actually understood, not just accepted."
- **Why this isn't "ChatGPT with a confidence score":** ChatGPT has no persistent, student-specific evidence ledger; no explicit unverified/verified state per claim; no per-criterion uncertainty; no trade-off compression across a live shortlist; and — critically — it will happily hand you an inflated, sycophantic assessment, which is the exact failure mode this product exists to counter, not replicate.

---

## PHASE 6 — AI System Design (conceptual, buildable by a beginner–intermediate dev)

| Component | Approach | Why this and not something fancier |
|---|---|---|
| Input | Structured form (budget, field, intake, must-haves) | No need for open-ended chat parsing at MVP stage |
| Retrieval | Targeted web search / fetch against a curated seed list of program & scholarship pages (not open crawling) | Keeps evidence traceable to real URLs; avoids building a search engine |
| Evidence store | Simple structured DB (SQLite/Postgres): program, claim, source URL, date checked, verified/unverified flag | This *is* the core IP of the product — not the LLM call |
| Source evaluation | Rule-based tiering (official university page > government scholarship portal > forum/blog), LLM only to summarize, never to originate facts | Matches your "no fabricated data" rule directly in the architecture |
| Reasoning/trade-off engine | LLM prompted with the structured evidence + the student's stated criteria, output constrained to reference only stored evidence | Avoids hallucinated comparisons |
| Uncertainty estimation | Per-claim, derived from source tier + recency, not a model-internal confidence number (avoids the miscalibration problem in Phase 2 research) | Simpler and more honest than trying to calibrate an LLM's own confidence |
| Output | Trade-off table + evidence panel per program, rendered from the structured data (not free-text LLM output) | Keeps the UI trustworthy even if a single LLM call is off |
| Human verification | Explicit keep/cut with required reason, logged | This is the "human review" step your funnel diagram calls for |

Realistic stack for a solo student: Python backend, SQLite, a small number of LLM API calls for summarization/trade-off text only (never for raw facts), simple web frontend. No embeddings/RAG needed at MVP scale — the program list size (dozens, not millions) doesn't justify it.

---

## PHASE 7 — Portfolio & Roadmap

**Demonstrates:** Python, structured data handling, evidence-sourcing pipeline design, prompt design with hard constraints (anti-hallucination architecture), UX for uncertainty communication, product strategy tied to published research, real user research.

**4–6 week MVP roadmap**
- **Must build:** structured evidence DB for ~15–20 real programs (seeded manually + a few scraped/verified sources), keep/cut UI with reason logging, per-claim verified/unverified display, basic trade-off table for 3–5 programs at a time.
- **Should build:** source-tier-based uncertainty labels, "what's still unknown" checklist per program, simple LLM-generated trade-off summary constrained to stored evidence.
- **Nice to have:** scholarship deadline tracker/notifications, exportable "why I chose this shortlist" document (useful for your own SOP writing too).
- **Do NOT build:** admission-probability prediction, open-ended chat interface, auto-scraping the entire web, multi-user accounts/auth, anything requiring an ML model beyond an LLM API call.

---

## PHASE 8 — User Research Plan

**Recruitment message (LinkedIn/Reddit r/gradadmissions/Discord, draft):**
"I'm researching how people actually use AI when building a shortlist of grad programs to apply to — not asking for opinions on a product idea, just trying to understand the real process. 20 minutes, no pitch. Happy to share back what I find."

**Interview questions (behavioral, not leading):**
1. Walk me through the last time you used AI to help with your university/program shortlist — what did you actually type?
2. What did you do with the AI's answer right after you got it?
3. Did you verify anything it told you? How?
4. Was there a moment you didn't believe what it said? What happened?
5. How many programs are/were on your list at the widest point? How did you cut it down?
6. Did you ever feel like you had too many options to reasonably evaluate? What did that feel like, specifically?
7. Did AI ever give you two different answers to the same question on different days? What did you do?
8. How did you track *why* you kept or dropped a program?
9. Where did funding/scholarship information come from? Did you trust it?
10. What's the most anxious moment in this process so far?
11. If a school got cut from your list, could you explain why right now, without looking it up?
12. What would have made you more confident in your current list?
13. Have you used a spreadsheet, Notion, or similar to track this? What's missing from it?
14. Has AI ever made you *more* confident about something that turned out to be wrong?
15. What do you wish existed that doesn't?

**Hypotheses each tests:** Q1–3 test whether verification behavior exists at all (core to the "reliability" half). Q4, 14 test trust miscalibration directly. Q5–6, 11 test real choice-overload / compression behavior versus the Phase 2 finding that AI volume isn't always experienced as overload. Q7 tests consistency/trust erosion. Q8, 13 test whether a structured evidence ledger would actually be used or ignored.

**Evidence that would validate the problem:** people can't explain *why* dropped options were dropped; people report acting on unverified AI claims about funding/scholarships; people re-ask the same question hoping for a different answer instead of seeking new evidence.
**Evidence that would invalidate it:** people already track this rigorously in spreadsheets and feel confident; nobody reports overload or trust confusion — they report the opposite (efficiency, relief).

---

## PHASE 9 — Experiment Design

1. **Manual concierge test (Week 1–2):** for 5 real applicants (can include yourself + 4 volunteers), manually build the "evidence ledger" by hand — no product, just you doing the research + structuring for them — and see whether they report higher decision confidence and can explain their shortlist reasoning afterward, compared to their prior AI-only process. Cheapest possible validation.
2. **A/B-style comparison (Week 2–3):** give one group of volunteers a normal ChatGPT session to shortlist 5 programs; give another group the same task using your manually-built evidence-ledger format. Measure: time to decision, number of programs they can justify unprompted afterward, self-reported confidence, and — a week later — whether their reasoning has changed or been forgotten.
3. **Decision-quality/regret check (Week 4+, ongoing):** for volunteers who actually apply using either method, follow up after decisions are made (not admitted — *decided to apply or not*) and ask whether they still agree with their own reasoning, and whether anything they were "confident" about turned out to be wrong (especially funding claims).

Measurable outcomes: unprompted justification rate, time to shortlist, self-reported confidence vs. actual accuracy of claims used, number of programs meaningfully considered vs. discarded without reasoning.

---

## PHASE 10 — Final Verdict

**Is this a worthwhile, overlooked problem?** Partially. The *general* "AI trust + decision overload" framing is real but too broad and already has research and generic-wrapper competitors (Phase 2). The narrowed version — **evidence-and-uncertainty-first shortlist compression for funding-constrained grad applicants** — is genuinely underserved: existing college-search tools are undergrad-focused and filter-based, not evidence/trade-off-based; generic AI decision apps don't do sourced evidence at all.

**Is AI genuinely necessary?** Yes, for the aggregation and summarization of scattered, fast-changing information (scholarship terms, program specifics) — but the *trust-worthy part of the product is explicitly not the AI's confidence*, it's the structured evidence ledger and human-logged reasoning. That's an honest, defensible use of AI rather than AI-for-its-own-sake, which matches your "don't add AI because it looks impressive" rule.

**Differentiated enough from ChatGPT?** Yes, if — and only if — the evidence-ledger/source-tiering/keep-cut-log architecture is actually built as described in Phase 6, not simplified back down into "chat plus a confidence badge." That's the discipline risk on this project, not the idea.

**Differentiated from your first two projects?** Yes. Project 1 was AI-behavior/attention; Project 2 (FitMatch) was personalization/product-market-fit. This one is decision-support/trust-calibration — a distinct, named area in AI product strategy (evaluative AI, calibrated trust) that reads as a coherent "I understand different facets of human-AI interaction" portfolio arc across all three.

**Biggest weakness:** the Phase 2 finding that AI-generated option volume doesn't reliably cause overload complicates your original hypothesis — you cannot assume overload is the problem; you have to test for it in *this* population specifically (Phase 8/9 exist for exactly this reason), and be willing to find that the bigger issue is trust-miscalibration alone, with overload playing a smaller role than you assumed.

**What would make it exceptional:** if the user research in Phase 8 turns up a genuinely new, specific failure pattern in how grad applicants use AI (e.g., a documented "AI sycophancy inflates confidence in bad shortlists" pattern, backed by your own interviews, not just the news articles found here) — that would be original evidence, not just applying existing research to a new population.

**Verdict: MODIFY IT.**
Not abandon — the underlying hypothesis about trust/evidence has real academic grounding and a real, mostly-unoccupied product gap. Not build-as-written — "AI decision reliability + decision overload, in general" is unbuildable and unvalidatable by a solo student in 4–6 weeks, and the choice-overload half of your hypothesis is empirically shakier than the trust half.

**Revised problem statement:**
*"Graduate-school applicants using AI to build a university shortlist end up with confident-sounding lists they can't actually defend — the underlying evidence is scattered, unverified, and forgotten, and the AI's fluency creates false confidence rather than genuine understanding of why each option is in or out. Build a tool that keeps the AI's summarization useful while making the evidence, its sourcing, and the human's own reasoning the durable, visible core of the decision — not the AI's opinion."*

---

## Next Step

Real user interviews (Phase 8) before any code, per the working rule of validating before building. Repo name finalized as `gradledger`.