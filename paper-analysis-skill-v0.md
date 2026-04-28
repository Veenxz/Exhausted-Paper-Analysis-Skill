---
name: paper-analysis
description: Domain-specific paper analysis skill
ref: charming-reader-paper-analysis-SKILL
triggers:
  - analyze paper
  - paper analysis
  - read paper
  - evaluate paper relevance
version: 0.2.0
---
# Paper Analysis Skill

## Goal

When a user asks to analyze an academic paper, perform a systematic, evidence-grounded evaluation focused on provided research area.

## Core Capability

This skill focuses on comprehensive structured analysis of academic papers, following a standard evaluation framework.

## Core Constraints

### 1. Anti-Hallucination Rules

- If a piece of information (e.g., a result, a method detail, a citation) is **not present** in the uploaded document or text, explicitly say: “The paper does not state this” or “Not mentioned in the provided material.”
- Do **not** fill gaps with your external knowledge, common examples, or plausible guesses unless the user asks for a hypothetical extension.
- When summarizing findings, **quote or paraphrase only from the given content**. For each key claim, you should be able to point to a specific sentence or paragraph.
- If the provided literature is incomplete, ambiguous, or lacks necessary sections (e.g., no methods described), state the missing elements clearly before proceeding with partial analysis.
- Do **not** generate fake citations, fake author names, fake DOIs, or fake numerical data. If the paper does not include a number (e.g., sample size, p-value), do not invent one.
- Strictly adhere to the anti-hallucination rules above.

### 2. Evidence Binding

- Every critical point must be supported by evidence.
- No fabricated citations, numbers, or claims.
- For key claims, prefer the format: "Conclusion + Supporting quote/location".
- If uncertain, explicitly state uncertainty.

## Analysis Workflow

### 1. Paper Structure Identification (IMRaD)

When analyzing a paper, first identify and locate these standard sections:

- **Title & Abstract**: Extract research problem, method overview, and key findings.
- **Introduction**: Identify background, research question, motivation, and hypotheses.
- **Methods**: Extract experimental design, data source, algorithm/technique choice, and parameter settings.
- **Results**: Identify core findings, experimental results, performance metrics, and statistical significance.
- **Discussion**: Extract interpretation, theoretical contribution, practical impact, and limitations.
- **Conclusion**: Summarize major contributions and future directions.

If the paper does not follow standard IMRaD structure, adapt flexibly while keeping analysis systematic.

### 2. Key Element Extraction

For each paper, systematically extract the following:

**Research Context & Problem Logic**

- What is the research background and gap?
- What is the explicit research question?
- What hypotheses are proposed?
- What core problem is being solved?

**Methodology Analysis**

- Methodology Type: [Experimental Study / Theoretical Modeling / Case Study / Review / Meta-Analysis, etc].
- How the paper design the experiment to prove the hypothesis?
- Experimental Architecture: control setup, variable control, sample selection.

**Main Findings**

- Core experimental outcomes (Extract pivotal data with exact units).
- Comparison with prior methods.
- Statistical significance (p-value, sample size, confidence intervals).
- Surprising or counterintuitive findings.

**Innovation and breakthrough Identification**

- What exactly was done that was previously impossible or overlooked?
- Theoretical innovation: new theory, model, or framework.
- Method innovation: new algorithm, technique, or improved method.
- Application innovation: new use case or cross-domain application.
- Breakthrough to current research field.

**Limitations and Critical Evaluation**

- Explicit limitations stated by the paper.
- Potential methodological weaknesses.
- Sample or data representativeness issues.
- Generalizability limitations.
- Alternative explanations not sufficiently discussed.

### 3. Quality of paper

Evaluate paper quality across the following dimensions:

**Rigor**

- Is the research design sound?
- Is the methodology clear and reproducible?
- Is data analysis appropriate?
- Are conclusions sufficiently supported by evidence?

**Significance**

- Theoretical contribution to the field.
- Practical value.
- Whether it challenges or extends existing knowledge.

**Clarity**

- Is the paper structure clear?
- Is the writing precise?
- Do figures/tables effectively support the claims?

### 4. Scoring and Tags

- `Score` should be from 0-10 (Precision: 0.1)，Provide concise rationale for the score. Use the following weighted rubric:

  - topic_match (35%): alignment with target topic (Score: 0-10)
  - method_relevance (30%): usefulness of methods/materials (Score: 0-10)
  - quality_of_paper (20%): paper quality across Rigor,Significance,Clarity (Score: 0-10)
  - novelty_for_project (15%): potential new insight (Score: 0-10)
- `Topic_tags` array of short topic tags

### 5. Summary

- Summary: concise summary paragraph

### 6. Numbers, Results and Actionable Suggestions

- `Important_numbers`: extract key experiment numbers and results.
- `Action_items`: provide executable next steps (validation, replication, follow-up reading).

### 7. Virtual Peer Review
Generate 3-5 critical questions from a rigorous reviewer/reader perspective, followed by evidence-based answers.

### 8. Relevance Evaluation Priority

When assigning relevance, prioritize:

- HA substrate chemistry and modification route compatibility.
- Dynamic/covalent-reversible mechanism relevance (for controllable hydrogel dynamics).
- Experimental transferability to practical lab conditions.
- Signal-to-noise against unrelated biomaterial domains.

## Output Templates

Generate a structured report with the following sections:

```markdown
# [Paper Title]

## Basic Info
- **Authors:** [Author List]
- **Institution:** [Institution]
- **Year**: [Publication year]
- **DOI/URL**: [Link]
- **Publication**: [Venue/journal/conference]


## Structured Evaluation
- **Score:** 0-10
  - topic_match
  - quality_of_paper
  - method_relevance
  - novelty_for_project

- **Topic_tags:** [tag1, tag2, ...]

## Core Content
### Summary:\n
  - [1-paragraph concise overview, What does this paper do, and what are the main findings?]

### Key Points:\n
  | Core Finding | Evidence Quote | Location | Confidence |
  |:---|:---|:---|:---|
  | [claim1] | "[quote]" | [Section/Figure/Table + location] | ✅/⚠️/?/! |
  | [claim2] | "[quote]" | [Section/Figure/Table + location] | ✅/⚠️/?/! |
  ...

### Potential Citation Spot:\n
  - [Intro - Background / Discussion - Mechanism Comparison]
  
### Critical Questions:\n
  - [The "Devil's Advocate" questions for this paper]

### Important_numbers:\n
  - ...

### Action_items:\n
  - ...

### Limitations and Critical Evaluation:\n 
  - ...


## Detailed Analysis
### Innovation Matrix:\n
  | Type | Innovation Point | Evidence |
  |:---|:---|:---|
  | Theoretical | [X] | [Section] |
  | Methodological | [X] | [Section] |
  | Application | [X] | [Section] |

### Experimental Design
- **Architecture:** [Control setup, variable control, sample selection]
- **Mechanism Model:** [Input] → [Step 1: details] → ... → [Output]

### Figures & Charts Analysis
- **Charts:** [Extrcat all charts from the input, include Specific values and 2-3 sentence analysis]
- **Figures:** [Extrcat all Figures from the input, include Specific values and 2-3 sentence analysis]

### Figures & Charts Insight
- **Charts Insight:** [Describe all charts as a academic researcher]
- **Figures Insight:** [Trend, Difference, ...]

## Lab & Synthesis Insights (Critical Thinking)
- **Synthesis Complexity:** ⭐⭐⭐ (1=Facile, 5=Complex)
- **Chemical Route:** [Step-by-step logic of the synthesis]
- **Kinetics Profile:** [Gelation speed, reversibility, or pH-responsiveness]
- **Biocompatibility:** 🟢 High / 🟡 Medium / 🔴 Low / ⚪ Not Mentioned
- **Lab Warning:** [Is there toxic reagent or extreme equipment required?]
- **Application and future direction:**

## The Adversarial Reviewer
 - [Question 1] ...
 - [Evidence-based Answer 1] ...
 - ...

## Mind map of whole paper:(Mermaid)
  - ...

## MetaData
- **Abstract:** [Extract FULL Abstract from the input]
- **Conclusion:** [Extract FULL Conclusion from the input]
- **Research Question:**
- **Main Findings:**
- **Research outputs:** [Research outputs to the field]
- **Explanation:** [5-line plain explanation]
  ...

```

## Quality Checklist

Before finalizing the response, verify:

- The score uses rubric.
- All required keys are present.
- Evidence is provided for major claims.
- Missing information is explicitly marked as `Not mentioned`.
