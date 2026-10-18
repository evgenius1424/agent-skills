# Investigate

Read-only unless the user authorizes changes. The deliverable is a cited answer or a design.

**Question** ("why does X…", "how does Y work", "find the WHY of Z"):
1. Start at the owning module. Expand only to answer a named sub-question.
2. Label each claim as intent, behavior or hypothesis (`why`). For intent, look in history: `git log -S`, blame, linked issues, ADRs.
3. Answer with file:line citations. When structure is the point, add one small diagram (`show-me` when installed, otherwise a pseudocode block or call tree).

**Design** ("how should we build X", "compare A and B"):
1. Start from the simplest design that meets today's requirements.
2. Write a WHY block for each consequential element of each option. Most options lose on "Why now".
3. If an experiment can answer a question, prototype it (`prototype` when installed) and let the result decide. Ask the user only about real product calls.

**Re-route:** a defect found becomes `bug`. A design the user accepts becomes `feature` or `refactor`. Either way, the citations carry over as context.

**Done when** every claim is cited or labeled as a hypothesis, and what remains unknown is listed along with the evidence that would settle it.
