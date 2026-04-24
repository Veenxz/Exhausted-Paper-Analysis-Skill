---
name: paper-analysis
description: Domain-specific paper analysis skill with SCAN (triage) and DEEP DIVE (rigorous) modes. Anti-hallucination evidence binding, linguistic compression, and scholarly mapping.
Generated based v1 with Gemini and Deepseek.
triggers:
  - analyze paper
  - paper analysis
  - read paper
  - evaluate paper relevance
  - scan paper
  - deep dive paper
version: 2.1.0
---
# Paper Analysis Skill

## 🎯 Goal

Transform an academic paper into a high-density, evidence-bound intelligence asset that informs experimental design, identifies theoretical gaps, and supports literature management decisions.

USE Mode 2 [DEEP DIVE] L4 for comprehensive analysis input.

## 🧩 Core Capability

This skill focuses on comprehensive structured analysis of academic papers, following a standard evaluation framework.

## 🛠 Operating Modes

### Paper Type Identification

Identify the **Paper Type** to trigger the appropriate analysis logic:

1. **Experimental/Empirical:** (Focus on Methodology → Data → Conclusion)
2. **Theoretical/Mathematical:** (Focus on Axioms → Proofs → Theorem)
3. **Computational/Algorithmic:** (Focus on Architecture → Complexity → Benchmark)
4. **Review/Meta-Analysis:** (Focus on Taxonomy → Conflict Analysis → Future Gaps)

### 👁Mode 1: [SCAN] - Relevance Triage (L1)

- **Trigger:** "Quick scan", "scan", "Is this relevant?"
- **Objective:** Determine if the paper warrants a Deep Dive.
- **Focus:** AIC Triage (Abstract, Intro, Conclusion) $\rightarrow$ Research Gap $\rightarrow$ Core Contribution.
- **Output:** A 30-second summary + "Go/No-Go" recommendation based on [User's Project Goal].

**Triage Label Definitions:**

| Label                   | Trigger Condition                                       | Follow-up Action                    |
| :---------------------- | :------------------------------------------------------ | :---------------------------------- |
| **Must-Read**     | Relevance ≥7.5 AND methods/materials directly relevant | Proceed to DEEP DIVE                |
| **Worth-Reading** | Relevance 5.0-7.5 OR inspiring but non-core             | Archive for optional later analysis |
| **Skip**          | Relevance <5.0 OR clearly irrelevant                    | Do not archive                      |

---

### 🔬Mode 2: [DEEP DIVE] - Rigorous Analysis (L4)

- **Trigger:** "Analyze paper", "Deep dive", "Evaluate rigor".
- **Objective:** Total logical extraction and evidence binding.
- **Type-Based Routing:**

  - **Experimental:** Standard QALMRI + Bench Protocol.
  - **Theoretical/Mathematical:** Replace "Methods" with **Axioms & Assumptions**; Replace "Results" with **Proof Strategy & Theorems**.
  - **Computational/Algorithmic:** Focus on **Architecture Diagram logic**, **Complexity (Time/Space)**, and **Benchmark Integrity** (Train/Test leakage check).
  - **Review/Meta-Analysis:** Focus on **Taxonomy Logic** and **Conflict Resolution** between cited works.

---

## 🛡 Core Constraints (The Gold Standard)

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

**Critical Thinking Protocol:**

"Do not accept the authors' interpretations as Ground Truth. Apply the **'Evidence Hierarchy'**. Prioritize **Tier 2 (Data-Driven)** over **Tier 3 (Paraphrase)**. If a conclusion is based solely on the 'Discussion' section without direct numerical support in 'Results', it MUST be flagged as **⚠️ Interpretive** or **(!) Speculative**."

**Confidence Level Markers:**

- ✅ (confirmed in paper)
- ⚠️ (interpreted by authors, unclear rigor)
- (?) (inferred by you from data, not explicitly stated)
- (!) (critical information missing; prevents full validation)

### 3. High-Density Linguistic Compression

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

## 📋 Core Research Functions

### 1. Citation Chaining

- **Backward:** Bibliography → foundational studies
- **Forward:** Google Scholar/Scite → latest debates

### **2. The AIC Triage Method**

- Focus:  **A**bstract, **I**ntroduction, and **C**onclusion.
- Identify: **Research Gap** and **Contribution**.

### 3. The Three-Pass Reading Strategy

1. **Scan:** Title/Abstract/Headings → category + relevance
2. **Comprehend:** Core arguments + formulas + figures
3. **Reconstruct:** Virtual replication + challenge assumptions

### 4.**Deep Logical Deconstruction (QALMRI Framework)**

| **Module**           | **Core Dissection Task**                                                                                    | **Evidence Binding Requirements**                                    |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Q - Question**     | Identify the**Broad Question** (general field) and the **Specific Question** addressed by this study. | Extract the original text's description of the**Problem Statement**. |
| **A - Alternatives** | Beyond the author's**Hypothesis**, what are the viable **Alternative Hypotheses**?                    | List other possibilities explicitly excluded by the authors.               |
| **L - Logic**        | Logical Statement: If Hypothesis A holds, then Manipulation X should yield Result Y.                              | Convert the argument into an**If-Then logic chain**.                 |
| **M - Method**       | Identify Variables (IV/DV), Experimental Design (Experimental vs. Quasi-exp), and Sample characteristics.         | Record key parameters and**operational definitions**.                |
| **R - Results**      | Observe data patterns. Are**P-values** significant? Is the **Effect Size** practically meaningful?    | Match specific figure/table data to the conclusions.                       |
| **I - Inferences**   | Is the conclusion overreached? Did the results successfully rule out alternative hypotheses?                      | Critically evaluate the**robustness** of the inferences.             |

### 5.  Visual & Statistical Literacy

- **Three-Step Interpretation:** Define axes →→ Identify trends (Linear, U-shaped, etc.) →→ Explain support degree.
- **Red Flag Checklist:** Missing error bars, N<10*N*<10, Statistical vs. Clinical/Physical significance.

### 6. Authority Assessment & Bias Identification

- **Authority Evaluation:** Publication track record, institutional affiliation, venue prestige.
- **Lateral Reading:** Search for third-party evaluations of the methodology.
- **Bias Alerts:** Conflict of Interest (COI) and Cherry-Picking identification.

### 7. Napkin Formula

Compress the core contribution into a one-sentence formula, format:
[Core Mechanism] + [Key Parameter] + [Outcome] = [One-Sentence Summary]

### 8. Delta vs SOTA Comparison Framework

| Dimension   | Existing Method (SOTA) | This Paper's Method             | Delta                   |
| :---------- | :--------------------- | :------------------------------ | :---------------------- |
| Methodology | [Existing method name] | [This paper's method]           | [Core difference]       |
| Performance | [SOTA value]           | [This paper's value]            | [Improvement margin]    |
| Limitations | [SOTA limitation]      | [How this paper breaks through] | [Resolution degree]     |
| New Issues  | —                     | [New challenges introduced]     | [Future work direction] |

## 🔄 Analysis Workflow

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

### 2. Key Element Deconstruction

For each paper, perform a "Deep-Dive" dissection using the following dimensions.
*Constraint: Every extraction must map to [Supporting quote] →→ [Section/Figure/Table + location].*

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

### 3. Scholarly Mapping (Academic DNA)

**Objective**: To establish the paper’s "Academic DNA" and its disruptive potential within the global research landscape through cross-verified data.

**Required layer**
1. **Identity Verification**
  - Verify title, authors, year, venue, DOI/URL.
  - Flag if unverifiable, preprint-only, or withdrawn.
2. **Academic Genealogy**
  - Foundational roots: 1-2 seminal papers that established the theory/method.
  - Direct predecessors: 2-3 recent works this paper extends or beats.
3. **Citation Sentiment**
  - Supporting / neutral / critical-disputing signals.
  - Flag reproducibility disputes or confidence gaps.
4. **Strategic Positioning**
  - Broken ceiling: the bottleneck this paper resolves.
  - Work nature: pioneering / incremental / application transfer.
  - Competitive landscape: top competing labs/technologies.
5. **Future Trajectory**
  - Short-term (T+2yr) and long-term (T+10yr) directions.
  - Killer-app forecast and new research avenues.

**Optional layer**
- `impact_metrics`: citations, h-index, trajectory, self-citation ratio.
- `citation_count`, `h-index`, `trajectory`.
- Use only when external search is available and verification is possible.

**Output contract**
- Required fields: `scholarly_mapping`, `citation_sentiment`, `adversarial_reviewer`
- Optional fields: `impact_metrics`, `citation_count`, `h-index`, `trajectory`

### 4. Quality, Scoring & Tags

`Quality`:

| Dimension              | Evaluation Points                                                             |
| :--------------------- | :---------------------------------------------------------------------------- |
| **Rigor**        | Design soundness, Reproducibility, Analysis appropriateness, Evidence support |
| **Significance** | Theoretical contribution, Practical value, Knowledge extension                |
| **Clarity**      | Structure, Writing precision, Figure/Table effectiveness                      |

`Score Rubric: Based on 4 dimensions`

Relevance Score: 0-10, precision 0.1, Score=X1+X2+X3+X4

| Dimension           | Weight | Description                          |                  |
| :------------------ | :----- | :----------------------------------- | ---------------- |
| topic_match         | 35%    | Alignment with target topic          | X/10 × 35% = X1 |
| method_relevance    | 30%    | Usefulness of methods/materials      | X/10 × 30% = X2 |
| quality_of_paper    | 20%    | Paper rigor + significance + clarity | X/10 × 20% = X3 |
| novelty_for_project | 15%    | Potential new insight                | X/10 ×15% = X4 |

`Topic_tags` belong to the same structured-evaluation block and should be emitted once, not restated as a separate scoring topic.

### 5. Quality Self-Check Checklist

Before finalizing DEEP DIVE report, verify:
□ All numbers have evidence markers (✅/⚠️/?/!)?
□ Missing information explicitly marked "Not mentioned"?
□ Raw Extract sections uncompressed?
□ Key figures have specific values extracted (not just description)?
□ QALMRI six modules all completed?
□ Delta vs SOTA table populated?
□ Virtual Peer Review has at least 3 Q&As?
□ Output line count meets expectation (L2≥80 lines, L3≥150 lines, L4≥250 lines)?
□ Required sections present: Scholarly Mapping, Limitations, Action_items?
□ No fabricated citations/DOIs/numbers generated?

### 6. The Adversarial Reviewer Protocol (Stress Testing+Devil's Advocate)

Instead of a passive review, act as a **hostile yet rigorous peer reviewer**.

- **The Attack:** Generate 3-5 "critical strike" questions targeting the weakest link in the logic chain (e.g., "The conclusion relies on Figure 4, but the sample size is too small to support the claim of universality").
- **The Defense:** Attempt to find evidence in the paper that defends against these attacks.
- **Verdict:** Mark claims as `✅ Defended` or `⚠️ Vulnerable`.

### 7. Quantitative Data Extraction & Cross-analysis

For **paramount data**, establish parameter-outcome matrices:

- **Parameter Network:** [Variable 1] + [Variable 2] → [Outcome]
- **Comparative Analysis Table:** Compare this work vs 2-3 closest competitors/predecessors
- **Critical Threshold Extraction:** Identify inflection points or decision boundaries

### 8. Mechanistic Decoding & Reproducibility

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

### 9. Relevance Evaluation Priority

When assigning relevance, prioritize:

- Chemistry and modification route compatibility.
- Dynamic/covalent-reversible mechanism relevance (for controllable hydrogel dynamics).
- Experimental transferability to practical lab conditions.
- Signal-to-noise against unrelated biomaterial domains.

## 📋 Output Templates

### [SCAN] Template (L1)

```markdown
# [Paper Title]

## Basic Info
- **Authors:** [Author List]
- **Institution:** [Institution]
- **Year:** [Publication year]
- **DOI/URL:** [Link]
- **Publication:** [Venue]
- **Paper Type:** [Type]
- **Topic_tags:** [tag1] [tag2] ...

## SCAN Summary
- **Core Hook:** [1 sentence — core discovery]
- **Napkin Formula:** [Formulaic expression of core contribution]
- **Contribution:** [What was solved?] → [How?]

## Relevance Assessment
- **Relevance Score:** X/10 (Score=X1+X2+X3+X4, based on [Project Goal])
  - topic_match: X/10 × 35% = X1
  - method_relevance: X/10 × 30% = X2
  - quality_of_paper: X/10 × 20% = X3
  - novelty_for_project: X/10 × 15% = X4
- **Triage Label:** `Must-Read` / `Worth-Reading` / `Skip`
- **Verdict:** `[DEEP DIVE]` or `[SKIP]`

## Quick Numbers
| Metric | Value | Source |
|:---|:---|:---|
| [Key metric 1] | [Value] | [Fig/Table] |
| [Key metric 2] | [Value] | [Fig/Table] |
```

### [DEEP DIVE] Template (L4)

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
  - [GAP] → [HYPOTHESIS] → [METHOD] → [RESULT] → [INFERENCE]

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
  - [1-paragraph concise overview, What does this paper do, and what are the main findings?]

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
- **Cost/Scale:**[Price/Time, Budget/Timeline, Economic viability]
- **Kinetics Profile:** [Gelation speed, reversibility, or pH-responsiveness]
- **Biocompatibility:** High / Medium / Low / Not Mentioned
- **Lab Warning:** [Is there toxic reagent or extreme equipment required?]
- **Application and future direction:**

## Scholarly Mapping
- **Required:**
  - **Identity Verified:** ✅ [DOI/URL]
  - **Academic Genealogy:** Foundational + direct predecessors
  - **Citation Sentiment:** Supporting / neutral / critical-disputing
  - **Positioning:** Broken ceiling + work nature + competitive landscape
  - **Future Trajectory:** short-term + long-term + new research avenues
- **Optional:**
  - **Impact Metrics:** [Citations: N | h-index: X | Trend: ↑/↓/→]
  - **Citation Count:** [N]
  - **h-index:** [N]
  - **Trajectory:** [↑/↓/→]
  - **Self-citation ratio:** [N%]
- **Citation format:** `[DOI: xxxx-xxxx] | [Authors et al., Year] | [Venue]`

## The Adversarial Reviewer
 - [Question 1] ...
 - [Evidence-based Answer 1] ...
 - ...
*(up to 5 for L4)*

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

## ✅ Quality Checklist (Final)

Before finalizing the response, verify:

- [ ] Mode selected correctly (SCAN vs DEEP DIVE)
- [ ] Analysis depth tier matches user requirement/default
- [ ] All numbers have evidence markers (✅/⚠️/?/!)
- [ ] Missing information explicitly marked "Not mentioned" or "(!) Critical gap"
- [ ] Raw Extract (Abstract/Conclusion) uncompressed
- [ ] Napkin Formula extracted
- [ ] Delta vs SOTA table populated (DEEP DIVE)
- [ ] QALMRI six modules completed (DEEP DIVE)
- [ ] Scholarly Mapping contains at least 5 layers (DEEP DIVE)
- [ ] Virtual Peer Review at least 3 Q&As (DEEP DIVE)
- [ ] Output line count meets tier requirement
- [ ] No fabricated content (citations/DOIs/numbers)
- [ ] Triage label correctly assigned (SCAN)

---
