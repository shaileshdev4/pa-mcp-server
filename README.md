# PA Tools MCP — Prior authorization lifecycle

**Prior authorization workflow support — coverage check, documentation audit, chart-grounded justification, verification, appeals, peer-to-peer prep, PAS bundle path, and audit trail — exposed as an MCP server for Prompt Opinion BYO agents.**

Built for [Agents Assemble — The Healthcare AI Endgame](https://agents-assemble.devpost.com) (May 2026).

| Resource | Link |
|----------|------|
| **GitHub (this MCP + demo data)** | [github.com/shaileshdev4/pa-mcp-server](https://github.com/shaileshdev4/pa-mcp-server) |
| **Companion — Sepsis MCP** | [github.com/shaileshdev4/sepsis-mcp-server](https://github.com/shaileshdev4/sepsis-mcp-server) |
| **Prompt Opinion Marketplace** | [MCP listing](https://app.promptopinion.ai/marketplace/mcp/019d6d86-411d-79d8-b4a4-b06bcfcd55a5) |

The **PA Authorization Agent** (BYO) orchestrates these tools; judges attach **this MCP** in Launchpad and run the demo prompts below.

Also see the upstream Prompt Opinion community overview in this repo’s historical layout ([SHARP-on-MCP](https://www.sharponmcp.com/)).

---

## Elevator pitch

One clinician-style prompt can drive a full payer-aware PA packet: documentation completeness, payer-specific coverage intelligence, AI-generated justification with a **second-pass verification** layer, trials, appeals, peer-to-peer preparation, optional Da Vinci PAS-style submission, and FHIR audit events when approved.

---

## Demo data (synthetic — upload to Prompt Opinion)

Bundled under **`demo-data/`** at this repository root:

| Patient | Folder / files | Use |
|---------|----------------|-----|
| **Marcus Williams** | `demo-data/marcus-williams/` — `marcus_williams_clinical_notes.txt`, `marcus_williams_day3_clinical_update.txt`, `marcus_williams_culture_simple.txt`, `marcus_williams_fhir_bundle.json` | ICU sepsis, **UnitedHealthcare**, Meropenem / penicillin anaphylaxis narrative |
| **Jennifer Mitchell** | `demo-data/jennifer-mitchel/jennifer mitchell.txt` | Oncology **Aetna**, HD-MTX / ALL |

Upload contents as **`DocumentReference`** resources for each synthetic patient before recording.

---

## Demo prompts (testing / video — run in order)

Full narration and timing: **`DEMO_VIDEO_SCRIPT_FINAL.md`**.

```text
1. Run a full PA workflow for this patient, payer is UnitedHealthcare

2. Previous request was denied — step therapy not completed. Peer-to-peer review required within 24 hours.

3. Run a full PA workflow for this patient, payer is Aetna
```

Alternate generic opener:

```text
run a prior authorization workflow for this patient, payer is Aetna
```

---

## MCP tools (12)

| Tool | Purpose |
|------|---------|
| `GetPatientData` | FHIR-backed patient context and documents |
| `GetPatientAge` | Age utility |
| `GetPatientAllergies` | Allergy list |
| `CheckCoverageRequirements` | Payer rules, timelines, factors |
| `CheckDocumentationCompleteness` | Evidence checklist |
| `MatchClinicalTrials` | ClinicalTrials.gov v2 |
| `GenerateClinicalJustification` | PA letter generation |
| `VerifyPALetter` | Claim verification / safety score |
| `GenerateAppealLetter` | Denial-specific appeal |
| `PreparePeerToPeer` | P2P prep |
| `SubmitPARequest` | Da Vinci PAS-style bundle / reference submit |
| `CreatePAAuditRecord` | FHIR AuditEvent on approval |

---

## Architecture

```text
Prompt Opinion → BYO PA Authorization Agent → MCP Streamable HTTP
PA Tools MCP (FastMCP, Groq for letters/verification)
  → deterministic extraction in Python where implemented
FHIR workspace → DocumentReference reads; AuditEvent writes when configured
External → ClinicalTrials.gov API v2
```

---

## Quick start (local)

```bash
git clone https://github.com/shaileshdev4/pa-mcp-server.git
cd pa-mcp-server/python
cp .env.example .env
# set GROQ_API_KEY and any FHIR-related vars your deployment needs
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

**MCP URL:** `python/main.py` mounts the MCP app at **`/`**. Use the base URL your host exposes (some setups add **`/mcp`** behind a reverse proxy — match whatever Prompt Opinion’s MCP tester expects).

```bash
curl -i http://localhost:8000/
```

---

## Connect in Prompt Opinion

1. Add your **public HTTPS** MCP URL.
2. Enable **FHIR / SHARP** context so patient id and token reach tools.
3. Attach **PA Tools MCP** to the **PA Authorization Agent** (BYO).
4. Refetch tools — confirm **12** tools.

For **sepsis + PA** end-to-end, attach **[sepsis-mcp-server](https://github.com/shaileshdev4/sepsis-mcp-server)** as well.

---

## Safety

- Synthetic / de-identified demo data only unless you have proper agreements for PHI.
- Outputs are **decision support** — physician review before submission.
- Payer profiles are illustrative; not legal guarantees.

---

## License

MIT

---

*AI-generated clinical content requires licensed clinician review before operational use.*
