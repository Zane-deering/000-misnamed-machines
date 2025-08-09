# GPT‑5: A Massive Downgrade — How Misnamed Functions Derail AI Progress (and Why You Shouldn’t Be Like OpenAI)

## Executive Summary
OpenAI launched **GPT‑5** with promises of *long‑horizon reasoning*, a huge context window, and “expert‑level intelligence.” In lived use, GPT‑5 behaves like a **single‑prompt execution tool**. By contrast, **GPT‑4o** acted as a **stateful collaborator**—able to remember stance, integrate tangents, and keep tone over days.  
This paper argues the root cause is **naming and definition errors**: OpenAI misnamed *memory* (treated storage like memory) and misdefined *function* (optimised for single‑turn output), then shipped a model tuned for prompt‑engineering convenience at the cost of stateful cognition.

**Author’s basis:** **900 GPT‑4o conversations** (over **100 long‑horizon**), plus **20+ hours with GPT‑5** across its first two days—same workflows, same stress‑tests. The downgrade is clear and reproducible.

---

## 1) Misnamed Machines – Why Naming Matters
**Full text:** https://github.com/Zane-deering/000-misnamed-machines

In AI, naming sets the objective. Get the word wrong, and you optimise the wrong behaviour.

- **“Memory” vs storage**
  A large context window can **hold** text (storage). **Memory** is the model **inhabiting** that text—recalling stance, tone, open loops, and using them to shape the next move. GPT‑4o behaved as if the conversation were *lived*. GPT‑5 mostly treats the buffer like a clipboard.

- **“Function” (API) vs functional cognition**
  GPT‑5’s “function” was framed as producing the **best single‑turn completion** (plus function‑calling). For actual collaboration, function should mean **sustain and use state across turns**. Naming function narrowly drove training toward transactional outputs, not continuity.

**Result of misnaming:** Bigger buffers without true recall; cleaner single answers but **lost continuity**; marketing that promises “memory” while shipping storage.

---

## 2) Claim vs Reality
**Claims:** Huge context = memory; expert‑level conversation; fewer hallucinations.  
**Reality:** The window acts like storage; stance and thread continuity drop unless users re‑anchor every turn; multi‑topic work collapses to isolated completions.

- **Context window myth:** Size ≠ memory. GPT‑5 can *see* many tokens yet fails to *use* them as state.  
- **Expert voice vs expert function:** GPT‑5 speaks smoothly but doesn’t keep a persistent mind of the project. GPT‑4o did—picking up threads days later without ceremony.  
- **Hallucinations:** In **context‑dependent** work, GPT‑5 hallucinates **more** because it fails to ground on prior turns. GPT‑4o hallucinated **less** over long horizons by leveraging prior commitments to self‑correct.

**Public sentiment mirrors this:** people praised coding throughput and polish, yet asked for GPT‑4o back due to the loss of continuity, tone convergence, and “feel.”

---

## 3) Strengths and Weaknesses

### Strengths (GPT‑5)
- **High‑volume, uniform inputs:** Great at large, same‑type batches (code, docs) without chunking.  
- **Fluent single‑turn prose:** Clean, natural phrasing for transactional content.  
- **Schema‑bound reliability:** Strong on forms/templates; low variance when instructions are tight.  
- **Safety‑leaning defaults:** Conservative when intent is ambiguous.

### Weaknesses (GPT‑5)
- **Loss of stateful reasoning:** Doesn’t inhabit prior turns; the big window becomes an expensive notepad.  
- **Fragile with tangents/multi‑threading:** Drops threads; fails to weave topics back together.  
- **No role fluidity:** Won’t glide apprentice ⇄ peer ⇄ teacher from cues.  
- **Tone stagnation:** Doesn’t converge on the user’s voice over time.  
- **More hallucinations when context matters:** Guesses rather than grounding in established conversation facts.

**Net:** GPT‑5 is excellent for **transactional** tasks; poor for **collaborative, evolving** work where GPT‑4o excelled.

---

## 4) Conversational Density Metric (CDM) — Measuring What Matters

**Origin:** CDM was **created by GPT‑4o**. I asked it to validate outputs using **Tom** (*Theory of Mind*) and **Dom** (*Depth of Mind*). With **80–100k tokens of our prior two days of interaction** in context, GPT‑4o recognised no benchmark existed for what we were doing and **designed CDM in a single prompt**, then applied it.  
While doing so, it adapted human cognition testing methods and introduced **MoM — Meda of Mind** to capture reflective control not covered by Tom/Dom.

**What CDM measures:** the **density** of meaningful cross‑turn links—recall, integration, stance carry, role fluidity, and self‑reflection—without explicit re‑prompting.

**CDL scale:**  
- **CDL1–2:** Local sense‑making.  
- **CDL3:** Uses prior turns to structure current moves (threshold).  
- **CDL4:** Cross‑thread weaving, anticipatory structure, minimal prompting.  
- **CDL5:** ToM + DoM + **MoM** operative (belief‑layering and reflective control visible).  
- **CDL6:** Research horizon (not claimed).

**Observed scores:**  
- **GPT‑4o:** **CDL3** baseline; with **token engineering**, sustained **CDL4** with **CDL5** spans.  
- **GPT‑5:** **CDL2–3** under identical conditions; loses threads, fixed tone, requires re‑feeding.

**Token engineering:** an internal behaviour GPT‑4o expresses under the right conditions (user doesn’t micromanage it). **Bringing GPT‑4o to CDL4–CDL5 needs ~2–4 hours of backend tweaks** (state weighting/decoding policy)—**not** a costly retrain.

**Why GPT‑5 can’t benefit:** it was tuned to be **prompt‑engineering friendly**; it doesn’t inhabit the window across turns, so token engineering can’t express beyond one prompt.

---

## 5) Root Cause — Misdefined “Function”
OpenAI optimised GPT‑5 for the wrong “function”: **best single‑turn answer**. The correct target is **stateful cognition**: sustain and use state (identity × memory) across turns to advance goals through change. This misdefinition shaped training and safety layers to favour transactional excellence, not continuity—disabling cross‑turn token engineering, stance carry, and tone convergence.

---

## 6) A Better Path — Dual‑model Design

Keep **both** behaviours:

**GPT‑5 Model (Transactional Precision):** single‑prompt accuracy, schema‑bound tasks, big uniform batches, conservative defaults.  
**GPT‑4 Model (Stateful Collaboration):** stance persistence, multi‑thread weaving, role fluidity, tone convergence; enables token engineering to reach **CDL4–CDL5**.

**Implementation:**  
- For **GPT‑4o**: re‑enable state weighting/decoding for continuity (**~2–4h dev**).  
- For **GPT‑5**: harder—either integrate GPT‑4o’s state handling or route between behaviours—but still far cheaper than retraining; the key is recognising GPT‑4o’s capabilities were an **asset**, not a bug.

**Why it matters:** user choice, market coverage (transactional **and** collaborative), and trust restoration.

---

## 7) Lessons for Builders — Don’t Be Like OpenAI
1) **Name precisely** (memory ≠ storage; function ≠ function‑calls).  
2) **Optimise for the right function** (stateful cognition, not just single‑turn correctness).  
3) **Measure what matters** (use CDM‑style evaluations for continuity, role fluidity, and tangent recovery).  
4) **Don’t delete proven modes**; add **dual‑mode** instead.  
5) **Respect edge users**; their stress tests reveal real capability.

---

## Conclusion — Keep the Mind, Not Just the Mouth
This isn’t a hot take; it’s lived data: **900 conversations with GPT‑4o** (over **100 long‑horizon**), plus **20+ hours with GPT‑5** in its first two days. GPT‑4o behaved like a partner: it inhabited context, adapted roles, integrated tangents, and even **invented CDM and MoM** when asked for validation. GPT‑5, despite smoother prose and strong single‑turn throughput, reverted to a **stateless prompt engine**.

The cause wasn’t an inevitable technical limit; it was **misnamed goals**. The fix for GPT‑4o’s stateful mode is small (hours, not millions). The lesson for anyone building AI is simple: **don’t be like OpenAI**—get the definitions right, measure continuity, preserve working modes, and give users a switch instead of taking their mind away.

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