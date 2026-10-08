# Phase 02 — User Research Plan

**Status:** Plan only. No interviews have been run yet. Nothing in this document is a finding.

**Depends on:** [Phase 01 — Problem Validation](phase-01-problem-validation.md)

---

## 1. What this research is for

Phase 01 ended with a MODIFY verdict and one open empirical question: **does the problem actually exist in the way the desk research suggests, for this specific population?**

The research below is designed to test the problem, not to pitch a solution. Participants are never told about the proposed product.

### Core hypotheses

| ID | Hypothesis | Source of doubt |
|----|-----------|-----------------|
| H1 | Grad applicants use AI to build or cut their shortlist, and often act on its output without verifying it | Desk research only |
| H2 | Applicants cannot explain, unprompted, why a dropped program was dropped | Desk research only |
| H3 | Funding/scholarship claims from AI are the highest-risk area for unverified reliance | Assumption |
| H4 | Applicants re-ask AI the same question hoping for a different answer instead of seeking new evidence | Assumption |
| H5 | Applicants experience too many options as a real burden | **Weakest hypothesis.** Phase 01 found AI-generated volume is not reliably experienced as overload |
| H6 | Existing tracking methods (spreadsheet, Notion) leave a real gap around evidence and reasoning | Assumption |

H5 is the one I most expect might be wrong. If the research shows the problem is trust miscalibration and not overload, that changes what gets built, and that is a valid outcome.

---

## 2. Who to talk to

**Target participants:** people who are currently applying, or recently applied, to master's/graduate programs abroad.

**Include:** applicants from any country (India-based preferred but not required), at any stage from early research to post-decision.

**Exclude:** anyone who has not used AI at all in their process. (Note them as a data point, but don't interview them for this round.)

**Target number:** 8 minimum, 12–15 ideal.

**Screener questions (ask before booking):**
1. Are you applying, or have you applied, to a master's/graduate program abroad?
2. Roughly how many programs have you considered at the widest point?
3. Have you used an AI tool (ChatGPT, Gemini, Claude, etc.) at any point in choosing programs?

---

## 3. Recruitment

**Channels:** LinkedIn, Reddit (r/gradadmissions and similar), Discord/WhatsApp/Telegram applicant groups, personal network.

**Message (draft):**

> I'm researching how people actually use AI when building a shortlist of grad programs. I'm not pitching anything or asking for opinions on an idea, just trying to understand the real process. 20 minutes, no preparation needed, and I'm happy to share what I find. If you've applied or are applying to master's programs abroad, I'd love to hear from you.

**Rules for recruitment:**
- Do not describe the proposed product in the message.
- Do not offer incentives that bias answers (a thank-you is fine; payment tied to positive feedback is not).
- Note where each participant was recruited from, since self-selection from one community can skew results.

---

## 4. Interview guide

Format: 20–25 minutes, one-on-one, video or call. Take notes. Record only with explicit permission.

**Opening (read aloud):**
> I'm studying how people make decisions when applying to grad programs. There are no right or wrong answers, and I'm not testing you. If you don't remember something, that's fine. You can skip any question or stop at any time.

**Questions**

*Behaviour (what actually happened)*
1. Walk me through the last time you used AI to help with your program shortlist. What did you actually type?
2. What did you do with the answer right after you got it?
3. Did you check any of it? How?
4. Was there a moment you didn't believe what it told you? What happened next?
5. Did the AI ever give you different answers to the same question? What did you do?

*Volume and cutting down*
6. How many programs were on your list at the widest point?
7. How did you get from that number down to the ones you applied to (or plan to)?
8. Did you ever feel you had too many options to properly evaluate? What did that feel like?

*Evidence and reasoning*
9. Where did funding and scholarship information come from? How much did you trust it?
10. How did you keep track of why you kept or dropped a program?
11. Pick a program you dropped. Can you explain why, right now, without looking anything up?

*Confidence and regret*
12. Has AI ever made you more confident about something that turned out to be wrong?
13. What part of this process has been the most stressful?
14. What would have made you more confident in your current list?

*Close*
15. Is there anything about this process I haven't asked about that matters?

**Do not ask:**
- "Would you use a tool that...?"
- "Don't you think AI is unreliable?"
- Any question that names or describes the proposed product.

---

## 5. What each question tests

| Questions | Hypothesis tested |
|-----------|-------------------|
| 1, 2, 3 | H1: do people verify at all? |
| 4, 12 | H1, H3: trust miscalibration, including cases where AI was confidently wrong |
| 5 | H4: re-asking behaviour |
| 6, 7, 8 | H5: whether overload is actually experienced |
| 9 | H3: funding information risk |
| 10, 11 | H2, H6: whether reasoning is recorded and recoverable |
| 13, 14, 15 | Open discovery: surfaces problems this plan didn't anticipate |

---

## 6. What would validate or invalidate the problem

**Supports the problem** (counted only if observed in multiple participants, not one):
- Participants cannot explain why dropped programs were dropped (H2)
- Participants report acting on AI claims about funding or eligibility without checking (H1, H3)
- Participants re-ask AI repeatedly instead of finding new sources (H4)
- Participants lose track of where a fact came from (H6)

**Weakens or invalidates the problem:**
- Most participants already verify AI output and track sources rigorously
- Participants report confidence, not anxiety, about their shortlist
- Existing tools (spreadsheets, Notion) are described as sufficient
- Nobody reports being overwhelmed by option volume (this would kill H5 specifically, and is plausible)

**Decision rule, set in advance:**
If fewer than roughly a third of participants show the core pattern (unverified reliance plus an unrecoverable reasoning trail), the problem as framed is not strong enough to build around, and the project should be re-scoped or dropped. This threshold is a judgment call, set before any data exists to avoid moving the goalposts afterwards.

---

## 7. Ethics and data handling

- Get verbal consent at the start; record only with explicit permission.
- Do not collect names, contact details, or personal identifiers in notes. Use participant codes (P01, P02, ...).
- Do not store admission results, grades, or financial details.
- Participants can withdraw at any time and have their notes deleted.
- Quotes used in the case study are anonymised and used only with permission.

---

## 8. Honest-reporting rules for this phase

- Every claim in later docs that comes from an interview must trace back to a specific participant code in the log below.
- No invented quotes, no composite quotes, no rounding "a few people" up to "most."
- Negative results and disconfirming answers get logged with the same prominence as supportive ones.
- If a hypothesis is wrong, the later docs say so plainly.

---

## 9. Timeline

| Week | Activity |
|------|----------|
| 1 | Post recruitment message, book first interviews |
| 1–2 | Run 8+ interviews, log each one within 24 hours |
| 2 | Synthesize against the hypotheses table, apply the decision rule |
| 2 | Write Phase 03: findings and decision (continue, re-scope, or stop) |

---

## 10. Interview log

*Empty until real interviews happen. Add one entry per participant.*

| Code | Date | Recruited from | Stage of applications | Used AI? | Notes file |
|------|------|----------------|----------------------|----------|-----------|
| | | | | | |