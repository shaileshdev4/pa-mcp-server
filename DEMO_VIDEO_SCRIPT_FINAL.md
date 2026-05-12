# PA Authorization Agent — Final demo script (Agents Assemble hackathon)

**Target runtime:** 2:50 · **Hard limit:** 3:00  

Use with **BYO — PA Authorization Agent** on Prompt Opinion, **PA Tools MCP** attached (12 tools). Synthetic patients only.

---

## Testing prompts (copy-paste — run in order)

Use after uploading bundled **`demo-data/marcus-williams/`** as FHIR **`DocumentReference`** content for **Marcus Williams** (see **`README.md`** in this repository).

### Marcus Williams — run 1 (full PA packet)

```text
Run a full PA workflow for this patient, payer is UnitedHealthcare
```

### Marcus Williams — run 2 (denial → appeal → peer-to-peer)

```text
Previous request was denied — step therapy not completed. Peer-to-peer review required within 24 hours.
```

---

## MCP tools you should see (actual names)

Typical trace for run 1 includes (order may vary by agent):

| Display / shorthand | Registered tool name |
|---------------------|----------------------|
| Patient chart | `GetPatientData` |
| Coverage | `CheckCoverageRequirements` |
| Documentation audit | `CheckDocumentationCompleteness` |
| Trials (optional) | `MatchClinicalTrials` |
| PA letter | `GenerateClinicalJustification` |
| Safety pass | `VerifyPALetter` |

Denial flow adds: `GenerateAppealLetter`, `PreparePeerToPeer`.

---

## Pre-recording checklist

- [ ] **Marcus Williams** — documents uploaded and verified in PO (see `demo-data/marcus-williams/`).
- [ ] **PA Authorization Agent** set as default for the session.
- [ ] Browser zoom **110%** (text readable on recording).
- [ ] **Do Not Disturb** on; only PO tab needed.
- [ ] **Test run** completed — Marcus run 1 + denial flow outputs clean (no raw JSON on screen if avoidable).
- [ ] Script printed — **do not read from this screen while recording** (use printed copy or teleprompter).

---

## Timing map

| Block | Time | Content |
|-------|------|---------|
| Hook | 0:00–0:22 | Voice only — PA burden + “under sixty seconds” |
| Problem / setup | 0:22–0:42 | PO open, patient list, Marcus, PA agent selected |
| Trigger | 0:42–0:55 | Type Marcus prompt 1, let tools show ~5 s |
| Marcus run 1 | 0:55–1:45 | Scroll packet — coverage, docs 100%, letter, verify ~0.7, allergies |
| Marcus run 2 | 1:45–2:20 | Denial prompt → appeal → P2P prep (**payer:** UnitedHealthcare for Marcus) |
| Close | 2:20–2:50 | MCP ×12, standards, marketplace, CTA |

---

## Full script (narration)

### [0:00 – 0:22] Hook

Voice only. Calm. Let numbers land.

> “A physician in the United States spends thirteen hours every week on prior authorization paperwork — not treating patients — filling out forms to convince insurance companies to approve treatments that have already been prescribed.  
> We built an AI agent that does the entire thing in under sixty seconds.”

---

### [0:22 – 0:42] Setup

Screen: PO Launchpad; **Marcus Williams** visible.

> “This is Prompt Opinion — a multi-agent healthcare platform built on MCP, A2A, and FHIR standards.  
> Marcus Williams. Fifty-eight years old. Sepsis. ICU.  
> He needs Meropenem — a carbapenem antibiotic — authorized immediately. Standard first-line therapy is contraindicated. I’ll explain why in a moment.”

**Do:** Click **Marcus Williams** → select **PA Authorization Agent**.

---

### [0:42 – 0:55] Trigger

> “One sentence.”

**Type (Marcus run 1 prompt):**

```text
Run a full PA workflow for this patient, payer is UnitedHealthcare
```

Hit Enter. Let tool calls show **~5 seconds** without talking over the list.

> “The agent is reading his FHIR clinical record, checking UnitedHealthcare’s coverage rules, auditing every required document…”

Let tools continue; avoid dead air (see “If tools are slow” below).

---

### [0:55 – 1:45] Marcus — first PA run

Scroll slowly; narrate sections as they appear.

**On packet header**

> “Full packet. In under sixty seconds.”

**On coverage — approval likelihood**

> “UnitedHealthcare. Seventy-two hour urgent decision window. Approval likelihood: medium-high — because complete clinical documentation is present.” *(Adjust wording to match live output.)*

**On documentation completeness — pause ~2 s if you hit 100%**

> “One hundred percent. Every required item — clinical notes, ICD-10 codes, physician attestation, medical necessity statement. Nothing missing.” *(If score &lt;100%, narrate honestly: “missing items flagged — that’s the point of the checklist.”)*

**On clinical justification — Meropenem / allergy paragraph**

> “Here is the letter.”

Read **from the screen** (paraphrase if your live letter differs):

> “Meropenem is medically necessary due to the patient’s documented history of penicillin anaphylaxis — which precludes standard first-line agents like piperacillin-tazobactam. Given septic shock trajectory — qSOFA three of three, lactate elevated — Meropenem is the appropriate empiric beta-lactam alternative per guideline-informed practice.”

Pause.

> “The agent read the penicillin allergy from the clinical record, identified that the standard antibiotic is contraindicated, and wrote the exception rationale — without being told to.  
> A template cannot do this. This is clinical reasoning.”

**On letter verification — safety score**

> “The agent then verifies every claim in the letter against the source data. Safety score and flagged lines — the physician sees exactly what to fix before signing.  
> That is the hallucination-detection layer. Every AI-generated letter gets reviewed before it reaches a physician’s desk.” *(Quote your actual score, e.g. 0.7, if shown.)*

**On allergy / contraindication summary**

> “Penicillin — anaphylaxis. Absolute contraindication. The agent knows this matters.”

---

### [1:45 – 2:20] Marcus — denial and response

**Type (Marcus run 2 prompt):**

```text
Previous request was denied — step therapy not completed. Peer-to-peer review required within 24 hours.
```

**On appeal**

> “Denial received. The agent immediately generates the rebuttal.”

Read a contraindication line **from the screen** if present.

**On peer-to-peer prep**

> “UnitedHealthcare often expects timely follow-up after denial — physicians go into peer-to-peer calls unprepared, against trained payer medical directors.  
> Here are talking points. Anticipated objections. Rebuttals. An opening strategy.  
> The physician walks into that call prepared.” *(Fix: original script said “Aetna” here — Marcus is **UHC**.)*

---

### [2:10 – 2:50] Close

> “Twelve MCP tools on one patient arc — approval, denial, appeal, peer-to-peer prep. Built on open standards — MCP, FHIR R4, CMS-0057-F alignment for future payer FHIR APIs.  
> The PA Authorization Agent is in the Prompt Opinion Marketplace. Any FHIR-connected patient context you authorize in the workspace — seconds to a draft packet.  
> Prior authorization doesn’t have to be medicine’s most expensive paperwork problem.”

**Hard cut.** No music required.

---

## Narration notes

- **Pace:** Hook — one sentence at a time. Demo — conversational, look at the screen naturally.
- **Lines to practice:** “A template cannot do this.” / “Patient safety versus coverage.” / “Prepared for peer-to-peer.”

### What not to say

- “As you can see…”  
- “I hope this demonstrates…”  
- “This is just a demo…”  
- “We’re working on…” (save for written “What’s next”)

### If tools are slow (&gt;8 s)

Keep narrating: *processing chart → coverage check → documentation audit → letter generation → verification.*

---

## Scroll order (editor’s shot list)

1. Patient list → Marcus selected  
2. PA Authorization Agent selected  
3. Prompt → tool calls (`GetPatientData`, `CheckCoverageRequirements`, …)  
4. Prior authorization packet header  
5. Coverage → approval factors  
6. Documentation completeness → pause if strong score  
7. Clinical justification → allergy / Meropenem paragraph  
8. Letter verification → safety score  
9. Allergy / contraindication summary  
10. Denial prompt → appeal → peer-to-peer  
11. End on clean output  

---

## Editing checklist

- [ ] Total **under 3:00**  
- [ ] No raw JSON on screen (collapse or scroll to narrative)  
- [ ] No error banners  
- [ ] 1080p, text readable  
- [ ] Clean audio  
- [ ] Captions (judges often watch muted)  

**YouTube title:** `PA Authorization Agent — Agents Assemble Hackathon 2026`  
**Visibility:** Unlisted or Public — copy URL into Devpost  

---

## Repository & companion submission

- **This MCP + demo files:** [github.com/shaileshdev4/pa-mcp-server](https://github.com/shaileshdev4/pa-mcp-server)  
- **Sepsis stewardship MCP (companion):** [github.com/shaileshdev4/sepsis-mcp-server](https://github.com/shaileshdev4/sepsis-mcp-server)  

Attach **both MCPs** to one BYO agent for end-to-end sepsis + PA demos.
