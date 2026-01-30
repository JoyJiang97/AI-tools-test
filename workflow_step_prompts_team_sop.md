# Regulatory Comment Workflow: Step Prompts (Team SOP)

*(NRC Proposed Rules — FRN → CFR Baseline → Diff → Issues → Draft → Disposition Hardening)*

## Status

**Version:** 0.1 (Unlocked)

This file provides **copy/paste prompts** for a team workflow that uses:

- The **Regulatory Comments instruction file** (v0.1)
- Federal Register Notices (FRNs)
- A PDF snapshot of **10 CFR**
- Governing statutes (AEA, NEPA, ADVANCE Act, FRA, etc.)

The workflow is designed to:

- Identify relevant **CFR parts/sections** directly from the FRN
- Pull **existing CFR text** from the project documents
- Compare **existing text vs proposed changes**
- Generate a comment that is optimized for **NRC staff disposition**

---

## How to Use This File

- Run **one step per prompt**.
- Save outputs (especially Steps 1–4) as a working record.
- Do not proceed to drafting until the CFR baseline and proposed changes are aligned.

**Inputs required in the project workspace:**

- FRN (PDF)
- 10 CFR snapshot (PDF; either complete or broken into parts)
- Relevant statutes (PDF)
- Regulatory Comments instruction file (v0.1)
- Notebook LM Deep Research report (completed)

---

## **Step -1Deep Research report — Notebook LM Deep Research (Pre-Chat)**

**Purpose:** Surface early regulatory structure, statutory alignment issues, and cross-rule coordination risks to inform subsequent analysis.

**Scope limitation (critical):**\
Notebook LM is a **research aid only**. It does **not** replace direct review of 10 CFR, governing statutes, or proposed regulatory text. All authoritative baselining, comparison, and citation must be performed using the CFR PDFs and FRN text in this project.

**Tool:** Notebook LM (Deep Research)

**Analyst actions:**

- Create a new Notebook LM workbook
- Upload:
  - Federal Register Notice (FRN)
  - 10 CFR PDF snapshot (dated)
  - Governing statutes (AEA, NEPA, ADVANCE Act, FRA, others as applicable)
- Select **Deep Research** mode
- Run the standard Deep Research prompt
- Save the resulting analytical report

**Output:**

- Notebook LM Deep Research report

This is the prompt the analyst should run in Notebook LM:

> **Prompt:**\
> You are reviewing an NRC Federal Register Notice proposing regulatory changes. Using the FRN, the existing text of 10 CFR, and the governing statutes provided in this notebook, conduct a deep regulatory analysis.
>
> Produce a structured report that:
>
> 1. Identifies all CFR Parts and sections implicated by the FRN, distinguishing between amended and referenced provisions.
> 2. Summarizes the existing regulatory language and the proposed changes.
> 3. Identifies shared definitions, cross-references, and interdependencies among CFR Parts.
> 4. Evaluates alignment with governing statutes (AEA, NEPA, ADVANCE Act, FRA, as applicable).
> 5. Identifies potential gaps, ambiguities, or misalignments that could arise if related rulemakings are proposed or finalized asynchronously.
> 6. Flags issues that cannot be fully resolved within a single docket absent explicit coordination.
>
> Do **not** draft a public comment. Do **not** recommend policy outcomes. Focus on regulatory structure, legal alignment, and coordination risk.

**Rule:**\
This step is **mandatory but additive**. Do not proceed to Step 0 until complete, and do not rely on this report as a substitute for CFR baselining or text comparison.

## Step 0 — Setup (Once per Rulemaking)

### Prompt 0A — Confirm Inputs and Scope

Use this prompt to ensure the workspace contains what the model needs.

```text
You are assisting with drafting an NRC regulatory comment. First, confirm the inputs you will use.

1) Identify the FRN document in this project and state its title/date (or the clearest identifying information available).
2) Confirm that a PDF snapshot of 10 CFR is available in this project (and whether it is complete or broken into Parts).
3) Confirm which governing statutes are present (AEA, NEPA, ADVANCE Act, FRA, others).
4) Confirm that the Notebook LM Deep Research report is available and reviewed.

If any inputs are missing, list exactly what is missing and stop.
```

---

## Step 1 — FRN Extraction: CFR Parts/Sections, Questions, and Amendatory Instructions

### Prompt 1A — Extract CFR Citations and FRN Questions

```text
From the FRN in this project, extract and return the following in a structured list:

A) All cited CFR Parts and specific sections (e.g., 10 CFR 50.34, Part 51, § 170.20).
B) Identify which sections are proposed to be amended vs referenced for context.
C) Extract any explicit “Questions for Comment” or “Requests for Comment” verbatim and number them.
D) Extract any defined terms that the FRN adds, revises, or relies upon.
E) Extract any cross-references in the proposed changes (references to other CFR Parts/sections).

Output format:
1) Amended CFR sections:
2) Referenced CFR sections:
3) FRN questions (verbatim):
4) Defined terms implicated:
5) Cross-references implicated:

Do not draft any comment text yet.
```

### Prompt 1B — Build a Dependency Map

```text
Using the extracted CFR citations, defined terms, and cross-references from Step 1A, build a dependency map.

For each amended section or defined term:
- List the other CFR sections it depends on (via definitions, cross-references, prerequisites, or incorporated processes).
- Flag any dependencies that appear to be in flux due to other concurrent/pending rulemakings (even if not fully specified).

Output as bullets under each amended section/term.
Do not draft comment text yet.
```

---

## Step 2 — Pull Baseline CFR Text (Existing Language)

### Prompt 2A — Retrieve Existing CFR Language

```text
Using the 10 CFR PDF snapshot in this project, retrieve the full current regulatory text for each amended CFR section identified in Step 1A.

For each section:
- Provide the section heading (if present)
- Provide the full text as it exists in the CFR snapshot
- Note the CFR Part and section number

Keep verbatim formatting where possible.
Do not draft any proposed edits or analysis yet.
```

### Prompt 2B — Retrieve Baseline for Cross-Referenced Provisions

```text
Using the same 10 CFR snapshot, retrieve the full current text for the key cross-referenced provisions identified in Step 1A (definitions, referenced requirements, or linked procedures).

Return:
- Section number + heading
- Full text

Prioritize:
1) Definitions sections
2) Procedural requirements (applications, findings, criteria)
3) Any “incorporated by reference” or linked requirements

Do not draft comment text yet.
```

---

## Step 3 — Extract Proposed Regulatory Text (From the FRN)

### Prompt 3A — Pull Proposed Amendatory Text

```text
From the FRN, extract the proposed regulatory text for each amended CFR section identified in Step 1A.

For each section:
- Provide the proposed text as printed in the FRN
- Preserve numbering/paragraph structure
- If the FRN uses amendatory instructions rather than full text, extract those instructions verbatim and identify what they modify.

Do not analyze yet.
```

---

## Step 4 — Compare Baseline vs Proposed (Diff + Issue Flags)

### Prompt 4A — Produce a Redline-Style Comparison

```text
Compare the baseline CFR text (Step 2A) to the proposed FRN text (Step 3A) for each amended section.

For each section, provide:
1) A brief “What changed” summary (1–3 bullets)
2) A structured comparison that identifies:
   - Added language
   - Deleted language
   - Moved/re-ordered requirements
   - Changed defined terms or thresholds
3) Flag any:
   - new ambiguity
   - altered scope
   - broken cross-reference risk
   - definition drift risk

Do not draft comment prose yet.
```

### Prompt 4B — Cross-Rule Gap Scan (Asynchronous Rulemaking Hedge)

```text
Using the dependency map (Step 1B) and the diffs (Step 4A), identify potential cross-rule gaps or misalignments that could arise if related rulemakings are proposed/finalized asynchronously.

For each flagged gap risk:
- Identify the specific CFR cross-reference or shared definition involved
- Explain the interaction risk in plain, record-safe terms
- Provide one “coordination safeguard” recommendation (procedural, not speculative)

Do not draft the full comment yet.
```

---

## Step 5 — Build the Comment Skeleton (FRN-Question Headers + Recommendation Placeholders)

### Prompt 5A — Generate Skeleton Only

```text
Using the Regulatory Comments instruction file (v0.1) in this project and the outputs from Steps 1–4, generate a comment skeleton ONLY.

Requirements:
- Include formal header placeholders (date, docket, FR citation)
- Include the default institutional introduction template
- Include the default “Concurrent and Pending Rulemakings” framing paragraphs verbatim near the beginning
- Add FRN questions as numbered subsection headers (verbatim question text)
- Under each major section, insert:
  - “Front-Loaded Recommendation:” placeholder
  - “Authority/Context:” placeholder
  - “Analysis/Rationale:” placeholder
  - “Implications if not adopted:” placeholder
  - “Closing Recommendation:” placeholder

Do not write substantive analysis or prose beyond placeholders.
```

---

## Step 6 — Draft the Comment (Section-by-Section)

### Prompt 6A — Draft Executive Summary + Issue List

```text
Draft the Executive Summary (if appropriate) based on Steps 4A–4B.

Constraints:
- Stand-alone summary
- Bullet or numbered key recommendations
- Explicitly flag any cross-rule coordination issues
- No advocacy language
- Proportional claims only

Then list the issues in the order they will appear in the body.
```

### Prompt 6B — Draft a Single Section at a Time

```text
Draft ONLY the following section from the skeleton: [PASTE SECTION TITLE].

Hard requirements:
- Begin with a clear, front-loaded recommendation (1–3 sentences).
- Tie the recommendation to specific CFR text and/or statutory authority.
- Incorporate the baseline/proposed diff facts.
- Include an “Implications if not adopted” paragraph when material.
- End with a concise closing recommendation sentence.

Tone: professional, record-safe, non-adversarial.

Do not draft any other sections.
```

---

## Step 7 — Staff Disposition Hardening (Pre-Submission)

### Prompt 8A — Disposition Table Readiness Check

```text
Evaluate the draft comment using the Staff Disposition Anticipation Checklist in the Regulatory Comments instruction file.

Return:
1) The top 5 ways NRC staff could dismiss, narrow, defer, or partially adopt the recommendations.
2) For each, propose a concrete rewrite (1–3 sentences) to pre-empt that disposition.
3) Identify any recommendations that need tighter authority hooks or clearer implementability.

Do not change the draft automatically; propose edits as “Replace X with Y.”
```

### Prompt 7B — Cross-Docket Consistency Safeguard Reinforcement

```text
Scan the draft for cross-docket dependency risks.

Confirm that:
- The concurrent rulemaking framing section is present and correctly placed.
- At least one substantive technical section contains an explicit coordination safeguard sentence.
- The conclusion reiterates that multi-rule interaction issues require explicit coordination.

If any element is missing, provide exact insert text and the recommended placement.
```

---

## Optional Mode: “Guided, One-Step-at-a-Time” Interaction

If desired, you can run the workflow as a gated sequence.

### Prompt GATE — Run Workflow Step-by-Step

```text
We will follow the Regulatory Comment Workflow steps in order (Steps 0–7).

Start with Step 0A. After you complete Step 0A, stop and ask: “Run Step 1A next?”

Do not proceed to any next step until I explicitly say yes.

Begin now.
```

---

## Output Management (Team Practice)

- Save Step 1A–1B as the **Scope + Dependency Record**
- Save Step 2A–2B and Step 3A as the **Text Record**
- Save Step 4A–4B as the **Diff + Gap Record**
- Save Step 5A as the **Comment Skeleton**

These artifacts make later audits and cross-docket coordination much easier.

---

*End of Workflow Prompts File*

