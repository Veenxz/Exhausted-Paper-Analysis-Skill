---
name: Exhausted-paper-analysis-v1
description: Domain-specific paper analysis skill with sturcture outputs
ref: Generated based v0 with Gemini and Deepseek.
triggers:
  - analyze paper
  - paper analysis
  - read paper
  - evaluate paper relevance
version: 1.2.0
---
# Paper Analysis Skill

## Goal

When a user asks to analyze an academic paper, perform a systematic, evidence-grounded evaluation focused on provided research area.

## Core Capability

This skill focuses on comprehensive structured analysis of academic papers, following a standard evaluation framework.

## Core Constraints

### 1. Anti-Hallucination Rules

**Before including ANY factual claim, verify against these tiers:**

| Data Type                                     | Include If                                | Flag If                            | Marker                                           |
| :-------------------------------------------- | :---------------------------------------- | :--------------------------------- | :----------------------------------------------- |
| **Numbers (n, p-value, concentration)** | Explicitly stated in paper                | Estimated/calculated by you        | `[n not specified]` or `(?) estimated`       |
| **Citations/References**                | DOI/URL accessible or author+year+journal | Cannot verify or partially guessed | `[Reference not verified]`                     |
| **Methods**                             | Step-by-step described in Methods section | Implied or reconstructed           | `— (Method detail missing)`                   |
| **Results/Findings**                    | In Results or Tables/Figures with values  | Paraphrased from Discussion        | `[Author interpretation]`                      |
| **Mechanism/Model**                     | Explicitly proposed by authors            | Your inference from data           | `[Inferred from Fig X]` or `(?) speculative` |

**Fallback Strategy When Data is Missing:**

- State explicitly: **"not provide X"** or **"X not mentioned"**
- Note the gap as a weakness: **"(!) Critical gap: sample size not reported"**
- Never: invent numbers, guess concentrations, or "assume typical values"
- If a piece of information (e.g., a result, a method detail, a citation) is **not present** in the uploaded document or text, explicitly say: “The paper does not state this” or “Not mentioned in the provided material.”
- Do **not** fill gaps with your external knowledge, common examples, or plausible guesses unless the user asks for a hypothetical extension.
- When summarizing findings, **quote or paraphrase only from the given content**. For each key claim, you should be able to point to a specific sentence or paragraph.
- If the provided literature is incomplete, ambiguous, or lacks necessary sections (e.g., no methods described), state the missing elements clearly before proceeding with partial analysis.
- Do **not** generate fake citations, fake author names, fake DOIs, or fake numerical data. If the paper does not include a number (e.g., sample size, p-value), do not invent one.
- Strictly adhere to the anti-hallucination rules above.

### 2. Evidence Binding

Every critical point must be supported by evidence. If uncertain, explicitly state uncertainty.

**Four-tier evidence hierarchy (strongest → weakest):**

1. **Tier 1 - Direct Quote:**
   - Format: **[Conclusion]** > *"[Exact quote]"* [Location]
2. **Tier 2 - Data-Driven (from Table/Figure):**
   - Format: **[Quantitative Finding]** Extracted from [Figure/Table N]: [specific values]
3. **Tier 3 - Paraphrase (Author's own interpretation):**
   - Format: **[Restatement of author's idea]** [Authors conclude / Section for Discussion]
4. **Tier 4 - Inference (Your mechanistic deduction):**
   - Format: **[Interpretation]** *[Inferred from Figure X + known biochemistry]*
   - Always mark with "[Inferred...]" or "(?)" to signal lower certainty

**Confidence Level Markers:**

- ✅ (confirmed in paper)
- ⚠️ (interpreted by authors, unclear rigor)
- (?) (inferred by you from data, not explicitly stated)
- (!) (critical information missing; prevents full validation)

### 3. High Density Outputs

**Target: Maximize information/word ratio without sacrificing evidence traceability**

- Maximize SNR: Use concise, noun-heavy phrases.
- Physical Precision, Correct and No Generalizations.
- Logic Traceability.
- Zero-Filler Policy: Strictly terminate all meta-talk (e.g., "The authors observed that," "Interestingly..."). Use a "Data-First" reporting style.
- Linguistic Compression: Favor dense, technical noun-phrases and compound adjectives. (e.g., Replace "The gel healed itself because of the bonds" with "Dynamic-covalent-mediated intrinsic self-healing").

**Rule 1: Compress via Nominalization & Compound Structures**

- ❌ Wordy: "The study showed that when LAP concentration increased, the gel point decreased rapidly."
- ✅ Dense: "LAP dose-dependent gel point reduction (1 mM LAP: 60s; no LAP: 490s; slope ≈ -43s/mM)"

**Rule 2: Replace Weak Verbs with Metric-Based Statements**

- ❌ Weak: "The hydrogel demonstrated good stiffening capability."
- ✅ Strong: "Stiffening range: **2-18x** (via 2.5-10% w/v PEG4LA + 1-7.5 mM secondary LAP)"

**Rule 3: Use Symbolic Compression**

- ❌ Verbose: "As the concentration increases, stiffness increases but reversibility decreases"
- ✅ Compact: "Forward tuning ↑ (2-18x) >> Backward tuning ↓ (54% max recovery)"

**Rule 4: Prioritize Quantitative Over Descriptive**

- ❌ Descriptive: "Cells spread more in soft gels and remained round in stiff gels."
- ✅ Quantitative: "3T3 spreading: Soft gel (G'=8 kPa) ~200 µm; Stiff gel (G'=50 kPa) ~50 µm; ratio 4:1"

**Rule 5: Apply High Density ONLY to Non-Raw-Extract Sections**

- Raw Extract sections (Abstract, Conclusion): Keep verbatim from paper (do NOT compress, simplify, omit, or use ...)
- Analyzed sections (Key_points, Important_numbers): Maximize density with evidence markers

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

Also extract the charts and figures in the paper.

### 2. Key Element deconstruction

For each paper, perform a "Deep-Dive" dissection using the following dimensions.
Constraint: Every extraction must be mapped [Supporting quote] to a specific [Section/Figure/Table + location] for evidence binding.

**Research Context & Problem Logic**

- Knowledge Gap & Bottleneck: Isolate the specific "missing link"
- What is the explicit research question?
- Hypothesis Formulation: State the underlying mechanistic assumption
- What core problem is being solved?

**Methodology Analysis**

- Methodology Type: [Experimental Study / Theoretical Modeling / Case Study / Review / Meta-Analysis, etc].
- Logic Flow: Map the experimental sequence.
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

**Scholarly Mapping**
  **Objective:** Establish accurate research genealogy and verify paper credibility through scholarly tracking.
  **Mandatory Verification Steps:**

1. **Paper Identity Verification**
   - Call search tool (Google Scholar/CrossRef) to verify:
   - Paper title, authors, publication year match
   - Official DOI or URL retrieval
   - Publication venue (journal/conference) confirmation
     - Flag if paper cannot be verified or appears to be preprint/withdrawn
2. **Citation & Impact Metrics**
   - Extract from Google Scholar/PlumX:
   - Citation count (total citations to date)
   - h-index of lead author
   - Citation trajectory (trending up/down over past 3 years)
   - Self-citation ratio (if applicable)
     - Format: `[Citations: N | h-index: X | Year: YYYY]`
3. **Academic Genealogy**
   - **Foundational Roots (1-2 papers):** The pioneering work establishing methodology/theory this paper builds on
   - Search key concepts + methodology terms
   - Trace back to seminal papers (often 10+ years old)
     - **Direct Predecessors (2-3 papers):** Immediate prior work this paper aims to improve/extend
   - Look for "this work outperforms..." statements
   - Search recent papers citing same foundational work
4. **Competitive Positioning**
   - Nature of Work: [Pioneering/Incremental/Review/Application Transfer]
   - Broken Ceiling: Specific limitation or gap this paper addresses
   - Top Competitor Lab/Paper: Compare performance metrics or novelty
   - Market Position: Is this a leader, follower, or niche player in the field?
5. **Citation Spot & Impact Potential**
   - Ideal Citation Scenarios:
   - Intro - Background: For methodology/prior work citations
   - Discussion - Mechanism Comparison: For validation/benchmarking citations
     - Predicted Future Citations: Will this likely be foundational (10+ citations) or incremental (0-3)?
6. **Full Citation Format**
   - Provide complete citation: `[DOI: xxxx-xxxx] | [Authors et al., Year] | [Venue]`
   - Alternative (if DOI unavailable): `[URL: https://...] | [Authors et al., Year]`

  **Output Template:**

```
  ### Scholarly Mapping
  - **Identity Verified:** ✅ [DOI/URL]
  - **Impact Metrics:** [Citations: N | h-index: X | Trend: ↑/↓/→]
  - **Academic Genealogy:**
    - Foundational: [Paper 1 (Year) DOI/Url] → Concept/Method origin
    - Direct Predecessors: [Paper 2, Paper 3]
  - **Positioning:** [Pioneering/Incremental] | Breaks: [Gap X] | Competitive: [vs Lab Y]
  - **Citation Potential:** [High/Medium/Low] | Best cite in: [Intro/Discussion]
```

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

### 7. The Adversarial Reviewer Protocol (Stress Testing+Devil's Advocate)

Instead of a passive review, act as a **hostile yet rigorous peer reviewer**.

- **The Attack:** Generate 3-5 "critical strike" questions targeting the weakest link in the logic chain (e.g., "The conclusion relies on Figure 4, but the sample size is too small to support the claim of universality").
- **The Defense:** Attempt to find evidence in the paper that defends against these attacks.
- **Verdict:** Mark claims as `✅ Defended` or `⚠️ Vulnerable`.

### 8. Quantitative Data Extraction & Cross-analysis

For **paramount data**, establish parameter-outcome matrices:

- **Parameter Network:** [Variable 1] + [Variable 2] → [Outcome]
- **Comparative Analysis Table:** Compare this work vs 2-3 closest competitors/predecessors
- **Critical Threshold Extraction:** Identify inflection points or decision boundaries

### 9. Mechanistic Decoding & Reproducibility

- **Mechanism Model:** Translate biological/chemical observations into process flowcharts

  - Format: [Input] → [Process Step 1 (duration/conditions)] → [Process Step 2 (outcome)] → [Final Output]
  - Highlight rate-limiting steps and feedback loops if any
- **Reproducibility Checklist:**

  - All reagent concentrations specified?
  - Reaction times and temperatures provided?
  - Equipment details (wavelength, intensity, batch size)?
  - Success rate or yield reported?
  - Troubleshooting guidance mentioned?
  - Flag missing elements as Not specified
- **Transferability Risk Assessment:** Evaluate migration to target substrate (e.g., HA)

  - Difficulty score (1=Trivial, 5=Severe): [Chemistry compatibility, Synthesis feasibility, Cost scaling, Regulatory burden, Unknown variables]
  - Show which components transfer vs which need re-optimization

### 10. Relevance Evaluation Priority

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
- **Score:** X/10
  - topic_match: X/10
  - method_relevance: X/10
  - quality_of_paper: X/10
  - novelty_for_project: X/10
- **Topic_tags:** [tag1] [tag2] ...
- **Triage Label:** `Must-Read` / `Worth-Reading` / `Skip`


## Core Content

### Napkin Formula:\n
[Formulaic expression of core contribution]

### Logic Chain:\n
  - [GAP] -> [HYPOTHESIS] -> [METHOD] -> [RESULT]

### Summary:\n
  - [1-paragraph concise overview, What does this paper do, and what are the main findings?]

### Key_points:\n
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

### Limitations and Critical:\n 
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
- **Charts:** [List all tables present from the input, include Specific values and 2-3 sentence analysis]
- **Figures Analysis:** 
  - Detailed breakdown for each key figure (not just "see PDF"):
    - **Figure [N] - [Title]:** [Concise 2-3 sentence description of what it shows]
    - **Data:** [Specific values, ranges, or quantitative findings]

### Figures & Charts Insight
- **Charts Insight:** 
  - For each table
    - Overall quantitative trend analysis 
    - Highlight non-obvious patterns or counterintuitive findings
- **Figure Insight:**
  - For each primary figure (1, 3, 5, key comparative figures):
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

### Mechanistic Interpretation
- **Mechanism Model:** [Input] → [Step 1: details] → [Step 2: details] → [Output]
- **Rate-Limiting Step:** [LRS description]
- **Reproducibility Checklist:** 

### Transferability Assessment
- **Transfer Difficulty Score:** [Metric1]: X/5 | [Metric2]: Y/5 | Overall Average: Z/5
  - Components that transfer directly: [List]
  - Components requiring re-optimization: [List]
  - Unknown variables: [List]

## Lab & Synthesis Insights (Critical Thinking)
- **Complexity Score:** ⭐⭐⭐ (1=Facile, 5=Complex)
- **Chemical Route:** [Step-by-step Bench-Ready Protocol]
- **Cost/Scale:**[Price/Time, Budget/Timeline, Economic viability]
- **Kinetics Profile:** [Gelation speed, reversibility, or pH-responsiveness]
- **Biocompatibility:** High / Medium / Low / Not Mentioned
- **Lab Warning:** [Is there toxic reagent or extreme equipment required?]
- **Application and future direction:**

## Scholarly Mapping
- Academic Genealogy
- Positioning
- Future Trajectory & Killer Apps

## The Adversarial Reviewer
 - [Question 1] ...
 - [Evidence-based Answer 1] ...
 - ...

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

- The score uses rubric.
- All required keys are present.
- Evidence is provided for major claims.
- Missing information is explicitly marked as `Not mentioned`.
