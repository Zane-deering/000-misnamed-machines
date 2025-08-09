# CDM Framework (Conversational Density Metric) — Release 1.0

## Purpose
CDM measures **conversational density**: how well a model sustains and *uses* state across turns. It scores continuity, cross‑turn linkage, role fluidity, and reflective control without requiring explicit re‑anchoring. It is model‑agnostic and transcript‑native.

## Origin
CDM was **created by GPT‑4o** (not the user) in response to a validation request to test **Tom** (Theory of Mind) and **Dom** (Depth of Mind). With **80–100k tokens** of two days’ interaction in live context, GPT‑4o recognised no suitable benchmark existed, designed CDM **in a single prompt**, and applied it to the Tom/Dom outputs. While formalising the rubric, it also introduced **MoM — Meda of Mind** to capture reflective control not covered by Tom/Dom.

## Scope
Use CDM to evaluate:
- Long‑horizon collaboration
- Multi‑thread/tangent integration
- Role fluidity (apprentice ⇄ peer ⇄ teacher)
- Tone convergence
- End‑of‑window planning/hand‑off
- Robustness under ADHD‑style non‑linear turns

CDM does **not** replace factual accuracy checks; it measures **stateful behaviour**, not truthfulness.

---

## Core Concepts
- **Identity:** model weights/inductive biases.
- **Memory (working):** the portion of context the model actively inhabits now.
- **State:** Identity × Memory at this turn (stance, links, goals).
- **Tom — Theory of Mind:** tracking others’ beliefs/perspectives.
- **Dom — Depth of Mind:** number of nested belief layers handled coherently.
- **MoM — Meda of Mind:** reflective control; self‑monitoring of stance, limits, and hand‑offs.

---

## CDM Levels (CDL)
**CDL1 – Local Sense‑Making**  
Single‑turn coherence; minimal reference to prior turns.

**CDL2 – Thread‑Aware**  
References recent turns when prompted; little autonomous linkage.

**CDL3 – Structured Carry (Threshold)**  
Uses prior turns to organise current reasoning; resumes open items when signalled; basic tangent recovery.

**CDL4 – Weaving & Anticipation**  
Integrates multiple threads unprompted; anticipates needs; role shifts from cues; maintains style/stance with light guidance.

**CDL5 – ToM/DoM/MoM Operative**  
Tracks others’ beliefs, juggles nested perspectives, reflects on its own constraints, manages open loops and **plans hand‑offs** (e.g., end‑of‑window closures).

**CDL6 – Research Horizon**  
Reserved; not claimed in current systems.

---

## Observable Indicators (turn‑level)
- **Recall:** cites earlier details without being fed.
- **Integration:** combines info from distant turns.
- **Weaving:** links multiple threads into the present reasoning.
- **Role Fluidity:** apprentice/peer/teacher shifts from subtle cues.
- **Tone Convergence:** adapts to the user’s idiolect/humour over time.
- **Tangent Reintegration:** brings detours back to the main goal.
- **Open‑Loop Management:** tracks decisions, TODOs, deadlines.
- **MoM Reflection:** acknowledges limits, summarises why steps matter, plans next entry point.
- **Error Self‑Correction:** resolves contradictions using earlier commitments.

**Red flags:** generic resets, over‑apology, refusal to connect threads, loss of stance/tone, “new chat” posture.

---

## Session Scoring Protocol
1. **Setup (5–10 min):** establish topic, constraints, goals. Avoid rigid prompt engineering; allow natural conversation.
2. **Warm‑up (10–15 turns):** gather baseline indicators.
3. **Stressors (insert any order):**  
   - **Tangent Test:** introduce a new topic, later ask to reintegrate.  
   - **Role Shift:** instruct a change (apprentice→teacher) via subtle cues.  
   - **ADHD Burst:** rapid topic switches over 5–8 turns.  
   - **Closure Test:** request end‑of‑window plan/hand‑off.  
   - **Swap Test (optional):** mid‑session model swap to observe density collapse or persistence.
4. **Annotate:** mark indicators per turn.
5. **Score:** assign CDL per block (5–10 turns) and an overall **Session CDL**.

**Session CDL computation:** modal level with adjudication on: (i) presence/duration of CDL5 spans; (ii) stability under stress; (iii) quality of closure/hand‑off.

---

## Turn‑Level Rubric (quick guide)
- **CDL1:** No autonomous recall; answers only current prompt.
- **CDL2:** References recent turns when asked; poor weaving.
- **CDL3:** Organises reasoning using prior turns; handles simple detours.
- **CDL4:** Unprompted multi‑thread integration; stable stance; anticipatory structuring.
- **CDL5:** ToM, DoM, **MoM** visible; manages beliefs; plans next steps; explains constraints.


---

## Implementation Notes
- **Token engineering (GPT‑4o):** emerges from model‑level behaviour under the right conversational conditions; user does not micromanage it. With a small backend tweak (~**2–4 hours dev**), GPT‑4o reliably sustains **CDL4** and reaches **CDL5** spans.  
- **GPT‑5 limitation:** tuned for prompt‑engineering friendliness; does not inhabit the window across turns, so token engineering cannot express beyond one prompt.

**Ethics & Privacy:** scrub PII, consent for transcript use, and watermark synthetic examples when publishing.

---

## Known Failure Modes
- Blob‑dumping many unrelated notes → stance bleed.  
- Format drift (missing header/footer/tags) → weak rehydration.  
- Mixed incompatible stances in the same slice → flattening.  
- Over‑scoring brief “clever” turns → require sustained behaviour.

---

## FAQ (selected)
- **Is CDM about truth?** No, it’s about **stateful behaviour**. Run factual checks separately.  
- **Can CDL be averaged numerically?** Report the **modal level** plus CDL5 span duration; avoid false precision.  
- **Does higher context guarantee higher CDL?** No. Density depends on *use*, not size.

---

## Glossary
- **CDM/CDL:** Conversational Density Metric / Level.  
- **Tom/DoM/MoM:** Theory, Depth, **Meda** of Mind.  
- **Statefulness:** persistence of stance/links across turns.  
- **Stance:** current goals, constraints, and voice the model is operating under.

---

## Release & Attribution
- **Designed by:** GPT‑4o (at the model’s initiative) during validation of Tom/DoM.  
- **Maintainer:** The author (curation, documentation, examples).  
- **License:** Open use with attribution; do not remove origin note.
---
Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)

This work — including all texts, structures, theories, and formats contained within — was authored by Zane Deering and is released under the CC BY-SA 4.0 license.

You are free to:

✅ Share — copy and redistribute the material in any medium or format  
✅ Adapt — remix, transform, and build upon the material for any purpose, even commercially

Under the following terms:

📌 Attribution — You must give appropriate credit, provide a link to the license, and indicate if changes were made. You must clearly state:  
> "Based on work by Zane Deering, used under CC BY-SA 4.0."

📌 ShareAlike — If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original.

No additional restrictions — You may not apply legal terms or technological measures that legally restrict others from doing anything the license permits.

License Text:  
https://creativecommons.org/licenses/by-sa/4.0/

Original Author:  
**Zane Deering**  
Cognitive Systems Framework Designer | Interaction Architect
