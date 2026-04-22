---
name: paper-analysis
description: Domain-specific paper analysis skill
ref: charming-reader-paper-analysis-SKILL
triggers:
  - analyze paper
  - paper analysis
  - read paper
  - evaluate paper relevance
version: 0.0.1
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

## Output Format

Generate a structured report with the following sections:

```markdown
# [Paper Title]

## Basic Info
- **Authors:** [Author List]
- **Institution:** [Institution]
- **Year**: [Publication year]
- **DOI/URL**: [Link]
- **Publication**: [Venue/journal/conference]
- **Paper Type:** [Experimental / Theoretical / Computational / Review]


## Structured Evaluation
- **Score:** X/10 (= X1 + X2 + X3 + X4)
  - topic_match: X/10 × 35% = X1
  - method_relevance: X/10 × 30% = X2
  - quality_of_paper: X/10 × 20% = X3
  - novelty_for_project: X/10 × 15% = X4
- **Topic_tags:** [tag1] [tag2] ...
- **Triage Label:** `Must-Read` / `Worth-Reading` / `Skip`


## Core Content

### Napkin Formula:\n
[Formulaic expression of core contribution]

### Logic Chain:\n
[GAP] → [HYPOTHESIS] → [METHOD] → [RESULT] → [INFERENCE]

### QALMRI Analysis:\n

| Module | Content | Evidence |
|:---|:---|:---|
| **Q - Question** | Broad: [X]; Specific: [Y] | [Section + quote] |
| **A - Alternatives** | H1: [X]; Alt: [Y] | [Section] |
| **L - Logic** | If [H1] then [Manipulation] → [Predicted Result] | [Inferred] |
| **M - Method** | IV: [X]; DV: [Y]; Design: [Z]; N: [N] | [Methods section] |
| **R - Results** | [Patterns, p-values, effect sizes] | [Fig/Table N] |
| **I - Inferences** | [Conclusion validity assessment] | [Evidence tier] |

### Summary:\n
[1-paragraph concise overview]

### Key Points:\n
| Core Finding | Evidence Quote | Location | Confidence |
|:---|:---|:---|:---|
| [claim1] | "[quote]" | [Section/Figure/Table + location] | ✅/⚠️/?/! |
| [claim2] | "[quote]" | [Section/Figure/Table + location] | ✅/⚠️/?/! |
...

### Delta vs SOTA Comparison:\n
| Dimension | SOTA | This Paper | Delta |
|:---|:---|:---|:---|
| Methodology | [Existing method] | [This method] | [Core difference] |
| Performance | [SOTA value] | [This value] | [Improvement] |
| Limitation Breakthrough | [SOTA limitation] | [How breakthrough] | [Resolution] |

### Important_numbers:\n
  - ...

### Action_items:\n
  - ...

### Limitations and Critical Evaluation:\n
- **Stated 1:** [Authors' own limitations]
- **Identified 1:** [Your critical observations]
- **Missing 1:** (!) [Critical gaps]
...


## Detailed Analysis

### Innovation Matrix:\n
| Type | Innovation Point | Evidence |
|:---|:---|:---|
| Theoretical | [X] | [Section] |
| Methodological | [X] | [Section] |
| Application | [X] | [Section] |

### Experimental Design
- **Architecture:** [Control setup, variable control, sample selection]
- **Mechanism Model:** [Input] → [Step 1: details] → [Step 2: details] → [Output]
- **Rate-Limiting Step:** [LRS description]
- **Reproducibility Checklist:**
  - □ Reagents specified? [Yes/No/Partial]
  - □ Times/temperatures? [Yes/No/Partial]
  - □ Equipment details? [Yes/No/Partial]
  - □ Yield/success rate? [Yes/No/Partial]
  - □ Troubleshooting? [Yes/No/Partial]

### Figures & Charts Analysis
| Item | Title | Data | Insight |
|:---|:---|:---|:---|
| Fig N | [Title] | [Specific values] | [2-3 sentence analysis] |

### Figures & Charts Insight
  - For each primary item (1, 3, 5, key comparative figures):
    - **[Figure #]:** [2-3 sentence analysis including: (a) what parameter changed, (b) observed outcome, (c) mechanistic implication]
    - **Comparison:** [If figures are sequential, note progression/relationship]
    - **Technical detail:** [Units, confidence levels, or methodology if visible]

### SWOT Analysis:
  - **Strengths:** [Why it works]
  - **Weaknesses:** [Methodological flaws/Data gaps]
  - **Opportunities:** [Potential follow-up experiments]
  - **Threats:** [Competitive technologies/Scalability issues]

### Quantitative Benchmark Tables
- **Parameter-Outcome Matrix:** (Key relationships)
  | [Variable 1] | [Variable 2] | [Outcome] | Fit Type | R²/p-value |
  |:---|:---|:---|:---|:---|
  | [Value1] | [Value1] | [Outcome1] | Linear | R²=X |
  
- **Comparative Analysis vs Competitors:**
  | Criterion | This Work | Competitor A | Competitor B | Winner |
  |:---|:---|:---|:---|:---|
  | [Metric1] | [Value] | [Value] | [Value] | ⭐ |

- **Critical Thresholds:** (Inflection points)
  - [Parameter]: <[Lower Bound] = ineffective; [Optimal Range] = best; >[Upper Bound] = toxic/undesired


## Transferability Assessment
- **Transfer Difficulty Score:** [Metric1]: X/5 | [Metric2]: Y/5 | Overall Average: Z/5
  - Components that transfer directly: [List]
  - Components requiring re-optimization: [List]
  - Unknown variables: [List]

## Lab & Synthesis Insights (Critical Thinking)
- **Complexity Score:** *** (1=Facile, 5=Complex)
- **Chemical Route:** [Step-by-step Bench-Ready Protocol]
- **Cost/Scale:** [Price/Time, Budget/Timeline, Economic viability]
- **Kinetics Profile:** [Gelation speed, reversibility, or pH-responsiveness]
- **Biocompatibility:** 🟢 High / 🟡 Medium / 🔴 Low / ⚪ Not Mentioned
- **Lab Warning:** [Is there toxic reagent or extreme equipment required?]
- **Application and future direction:**

## Scholarly Mapping
- **Identity Verified:** ✅ [DOI/URL]

### Academic Genealogy
| Tier | Paper | Contribution |
|:---|:---|:---|
| Foundational | [Author et al. ] | [Established theory] |
| Direct Predecessor | [Author et al. ] | [Provided A, lacked B] |
| This Work | Current paper | [Solves B] |

Papers:
List complete citation: `[DOI: xxxx-xxxx] | [Authors et al., Year]`
- Paper 1
...

### Citation Sentiment
| Type | Proportion | Representative Citation |
|:---|:---|:---|
| Supporting | X% | [Citation] |
| Neutral | X% | [Citation] |
| Critical/Disputing | X% | (!) [Citation] |

### Positioning
- **Broken Ceiling:** [Specific bottleneck resolved]
- **Work Nature:** [Pioneering / Incremental / Application Transfer]

### Future Trajectory & Killer Apps
| Timeframe | Predicted Direction |
|:---|:---|
| Short-term (T+2yr) | [Immediate extensions] |
| Long-term (T+10yr) | [Killer application] |
| New Research Avenues | [Sub-field opened] |

## The Adversarial Reviewer
 - [Question 1] ...
 - [Evidence-based Answer 1] ...
 - ...
*(up to 5)*

## Mind map of whole paper:(Mermaid)
[Mermaid diagram]

## MetaData
- **Abstract:** (Raw Extracts) [FULL - UNCOMPRESSED]
- **Conclusion:** (Raw Extracts) [FULL - UNCOMPRESSED]
- **Research Question:** [Exact]
- **Main Findings:** [Exact]
- **Research outputs:** [To the field]
- **Explanation:** [5-line plain explanation: Background - Problem - Method - Findings - Significance]
  ...

```

## Quality Checklist

Before finalizing the response, verify:

- [ ] All numbers have evidence markers (✅/⚠️/?/!)
- [ ] Missing information explicitly marked "Not mentioned" or "(!) Critical gap"
- [ ] Raw Extract (Abstract/Conclusion) uncompressed
- [ ] Napkin Formula extracted
- [ ] Delta vs SOTA table populated
- [ ] QALMRI six modules completed
- [ ] Scholarly Mapping contains at least 5 layers
- [ ] The Adversarial Reviewer has at least 3 Q&As
- [ ] No fabricated citations/DOIs/numbers generated
- [ ] Triage label correctly assigned
