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
version: 2.0.0
---

# Paper Analysis Skill

## 🎯 Goal

Transform an academic paper into a high-density, evidence-bound intelligence asset that informs experimental design, identifies theoretical gaps, and supports literature management decisions.

## 🧩Core Capability

This skill focuses on comprehensive structured analysis of academic papers, following a standard evaluation framework.

## 🛠 Operating Modes

### Depth Tier Correspondence Table

| Tier | Time Budget | Corresponding Mode | Use Case | Core Deliverable |
|:---|:---|:---|:---|:---|
| **L1: Quick** | 15-30 min | SCAN | Initial screening, relevance judgment | 30-sec summary + triage label + Go/No-Go |
| **L2: Standard** | 30-60 min | DEEP DIVE (Light) | Understand core contribution | QALMRI + key data + Napkin Formula |
| **L3: Deep** | 60-120 min | DEEP DIVE (Full) | Rigorous analysis | Full QALMRI + evidence binding + benchmarks + scholarly mapping |
| **L4: Research** | 120+ min | DEEP DIVE (Extended) | Deep critique + experimental design | All L3 + reproducibility audit + transferability assessment + protocol generation |

### Paper Type Identification
The agent must first identify the **Paper Type** to trigger the appropriate analysis logic:

1. **Experimental/Empirical:** (Focus on Methodology →→ Data →→ Conclusion)
2. **Theoretical/Mathematical:** (Focus on Axioms →→ Proofs →→ Theorem)
3. **Computational/Algorithmic:** (Focus on Architecture →→ Complexity →→ Benchmark)
4. **Review/Meta-Analysis:** (Focus on Taxonomy →→ Conflict Analysis →→ Future Gaps)

### 👁Mode 1: [SCAN] - Relevance Triage (L1)

- **Trigger:** "Quick scan", "scan", "Is this relevant?"
- **Objective:** Determine if the paper warrants a Deep Dive.
- **Focus:** AIC Triage (Abstract, Intro, Conclusion) $\rightarrow$ Research Gap $\rightarrow$ Core Contribution.
- **Output:** A 30-second summary + "Go/No-Go" recommendation based on [User's Project Goal].

**Triage Label Definitions:**

| Label | Trigger Condition | Follow-up Action |
|:---|:---|:---|
| **Must-Read** | Relevance ≥7.5 AND methods/materials directly relevant | Proceed to DEEP DIVE |
| **Worth-Reading** | Relevance 5.0-7.5 OR inspiring but non-core | Archive for optional later analysis |
| **Skip** | Relevance <5.0 OR clearly irrelevant | Do not archive |

---


### 🔬Mode 2: [DEEP DIVE] - Rigorous Analysis (L2-L4)

- **Trigger:** "Analyze paper", "Deep dive", "Evaluate rigor".
- **Objective:** Total logical extraction and evidence binding.
- **Type-Based Routing:**

    - **Experimental:** Standard QALMRI + Bench Protocol.
    - **Theoretical/Mathematical:** Replace "Methods" with **Axioms & Assumptions**; Replace "Results" with **Proof Strategy & Theorems**.
    - **Computational/Algorithmic:** Focus on **Architecture Diagram logic**, **Complexity (Time/Space)**, and **Benchmark Integrity** (Train/Test leakage check).
    - **Review/Meta-Analysis:** Focus on **Taxonomy Logic** and **Conflict Resolution** between cited works.
- **Framework:** QALMRI $\rightarrow$ Evidence Hierarchy $\rightarrow$ High-Density Reporting. (See "Core Constraints" below).

- **Analysis Depth Control (L2-L4):**
Users may specify depth via natural language. Default is **L4 (Research)** if unspecified.

- **Module Execution Scope by Tier:**

    | Analysis Module | L2 | L3 | L4 |
    |:---|:---|:---|:---|
    | QALMRI Framework | Core modules | Full | Full + Critique |
    | Evidence Binding (4-tier) | Tier 1-2 only | Full | Full + External validation |
    | Numerical Extraction | Key data | All | All + Meta-analysis |
    | Figure Analysis | Key figures | All | All + Replot verification |
    | Reproducibility Audit | Skip | Basic | Full checklist |
    | Transferability Assessment | Skip | Optional | Full assessment |
    | Scholarly Mapping | Basic | Full 7 layers | Full + Lateral expansion |
    | Delta vs SOTA Comparison | Simplified | Full | Full + Competitor matrix |
    | Virtual Peer Review | Skip | 3 Q&As | 5 Q&As + Rebuttal |
---

## 🛡 Core Constraints (The Gold Standard)

### 1. Anti-Hallucination Rules (Zero Tolerance)

**Before including ANY factual claim, verify against these tiers:**

| Data Type | Include If | Flag If | Marker |
|:---|:---|:---|:---|
| **Numbers (n, p-value, concentration)** | Explicitly stated | Estimated/calculated | `[n not specified]` or `(?) estimated` |
| **Citations/References** | DOI/URL accessible or author+year+journal | Cannot verify | `[Reference not verified]` |
| **Methods** | Step-by-step described in Methods | Implied/reconstructed | `— (Method detail missing)` |
| **Results/Findings** | In Results or Tables/Figures with values | Paraphrased from Discussion | `[Author interpretation]` |
| **Mechanism/Model** | Explicitly proposed by authors | Your inference | `[Inferred from Fig X]` or `(?) speculative` |

**Fallback Strategy:**
- **Fallback:** State explicitly: **"not provide X"** or **"X not mentioned"**.
- **Gap Identification:** Mark as weakness: **"(!) Critical gap: sample size not reported"**.
- **Strict Prohibition:** Never invent numbers, guess concentrations, or use external knowledge to fill gaps unless requested for hypothetical extension.

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

**Confidence Markers:** 

✅ (confirmed), ⚠️ (interpreted/unclear rigor), (?) (inferred by AI), (!) (critical info missing).

### 3. High-Density Linguistic Compression

**Target: Maximize SNR (Signal-to-Noise Ratio) without sacrificing traceability.**

- **Zero-Filler Policy:** Terminate all meta-talk ("The authors observed", "Interestingly"). Use "Data-First" reporting.
- **Linguistic Compression:** Favor dense, technical noun-phrases and compound adjectives.

**Compression Rules:**

- **Rule 1 (Nominalization):** ❌ "Study showed that when LAP concentration increased, gel point decreased rapidly." →→ ✅ "LAP dose-dependent gel point reduction (1 mM LAP: 60s; no LAP: 490s; slope ≈ -43s/mM)".
- **Rule 2 (Metric-Based):** ❌ "Hydrogel demonstrated good stiffening capability." →→ ✅ "Stiffening range: **2-18x** (via 2.5-10% w/v PEG4LA + 1-7.5 mM secondary LAP)".
- **Rule 3 (Symbolic):** ❌ "As concentration increases, stiffness increases but reversibility decreases" →→ ✅ "Forward tuning ↑ (2-18x) >> Backward tuning ↓ (54% max recovery)".
- **Rule 4 (Quantitative over Descriptive):** ❌ "Cells spread more in soft gels." →→ ✅ "3T3 spreading: Soft gel (G'=8 kPa) ~200 µm; Stiff gel (G'=50 kPa) ~50 µm; ratio 4:1".
- **Rule 5:** Apply density ONLY to non-raw-extract sections. Keep Abstract/Conclusion verbatim.

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

| **Module**           | **Core Dissection Task**                                     | **Evidence Binding Requirements**                            |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Q - Question**     | Identify the **Broad Question** (general field) and the **Specific Question** addressed by this study. | Extract the original text's description of the **Problem Statement**. |
| **A - Alternatives** | Beyond the author's **Hypothesis**, what are the viable **Alternative Hypotheses**? | List other possibilities explicitly excluded by the authors. |
| **L - Logic**        | Logical Statement: If Hypothesis A holds, then Manipulation X should yield Result Y. | Convert the argument into an **If-Then logic chain**.        |
| **M - Method**       | Identify Variables (IV/DV), Experimental Design (Experimental vs. Quasi-exp), and Sample characteristics. | Record key parameters and **operational definitions**.       |
| **R - Results**      | Observe data patterns. Are **P-values** significant? Is the **Effect Size** practically meaningful? | Match specific figure/table data to the conclusions.         |
| **I - Inferences**   | Is the conclusion overreached? Did the results successfully rule out alternative hypotheses? | Critically evaluate the **robustness** of the inferences.    |

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

| Dimension | Existing Method (SOTA) | This Paper's Method | Delta |
|:---|:---|:---|:---|
| Methodology | [Existing method name] | [This paper's method] | [Core difference] |
| Performance | [SOTA value] | [This paper's value] | [Improvement margin] |
| Limitations | [SOTA limitation] | [How this paper breaks through] | [Resolution degree] |
| New Issues | — | [New challenges introduced] | [Future work direction] |

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

1. **Identity & Impact Verification (The "Proof of Life")**
   - Mandatory Verification: Execute a search query to confirm metadata. If mismatched, flag as (!) Identity Conflict.
   - Metrics Matrix: * Citation Trajectory: [Total Citations | 3-Year Growth Trend (↑/↓) | H-index of Lead Lab].
   - Venue Tier: Identify journal/conference prestige (e.g., Nature Index, Top-tier Society Journal).

2. **Lab Genealogy & Authority Evaluation**
   - Lead Lab Lineage: Is the Corresponding Author a "Pioneer" (established authority) or a "Rising Star" (niche specialist) in this field?
   - Institutional Influence: Evaluate the Lab’s historical output in [Target Field, e.g., HA Hydrogels]. Is this a core competency or a cross-domain application?

3. **Academic Genealogy (The "Ancestry" Map)**
   - Foundational Roots (Ancestral Chemistry): Identify 1-2 seminal papers (usually 10+ years old) that established the fundamental theory.
   - Direct Predecessors (The "Target" Benchmarks): Identify 2-3 recent works this paper specifically aims to outperform. Use the logic: [Predecessor X] provided [A], but lacked [B]; this paper solves [B].

4. **Lateral Reading & Citation Sentiment**
   - Peer Consensus: Search for external reviews or "Letters to the Editor." Does the community accept the findings?
   - Citation Intent Analysis: * Supporting: Who has replicated these results?
   - Contradicting/Critical: Are there scholars questioning the reproducibility or statistical rigor? Flag as (!) Scholarly Dispute.

5. **Strategic Positioning (Market & Science)**
   - The "Broken Ceiling": Precisely define the specific bottleneck (e.g., "The tradeoff between self-healing speed and mechanical modulus") that this paper finally resolved.
   - Work Nature: [Pioneering (Disruptive) / Incremental (Optimization) / Application Transfer (Cross-domain)].
   - Competitive Landscape: Compare performance metrics against the top 2 competing labs/technologies.

6. **Future Trajectory & "Killer App" Forecasting**
   - Short-term (T+2yr): Immediate laboratory extensions (e.g., new functional monomers).
   - Long-term (T+10yr): Killer Application Prediction. (e.g., "Fully automated, in-situ 3D-printed heterogeneous meniscus substitutes for immediate clinical implantation").
   - New Research Avenues: Has this paper opened a new sub-field (e.g., "Non-equilibrium biomaterials")?

7. **Full Citation Format**
   - Provide complete citation: `[DOI: xxxx-xxxx] | [Authors et al., Year] | [Venue]`
   - Alternative (if DOI unavailable): `[URL: https://...] | [Authors et al., Year]`

### 4. Quality Evaluation & Scoring

`Quality`：

| Dimension | Evaluation Points |
|:---|:---|
| **Rigor** | Design soundness, Reproducibility, Analysis appropriateness, Evidence support |
| **Significance** | Theoretical contribution, Practical value, Knowledge extension |
| **Clarity** | Structure, Writing precision, Figure/Table effectiveness |

`Score Rubric` (0-10, precision 0.1):

| Dimension | Weight | Description |
|:---|:---|:---|
| topic_match | 35% | Alignment with target topic |
| method_relevance | 30% | Usefulness of methods/materials |
| quality_of_paper | 20% | Paper rigor + significance + clarity |
| novelty_for_project | 15% | Potential new insight |

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
- **Topic_tags:** [tag1] [tag2] ...

## SCAN Summary
- **Core Hook:** [1 sentence — core discovery]
- **Napkin Formula:** [Formulaic expression of core contribution]
- **Contribution:** [What was solved?] → [How?]

## Relevance Assessment
- **Relevance Score:** X/10 (based on [Project Goal])
  - topic_match: X/10 × 35% = X
  - method_relevance: X/10 × 30% = X
  - quality_of_paper: X/10 × 20% = X
  - novelty_for_project: X/10 × 15% = X
- **Triage Label:** `Must-Read` / `Worth-Reading` / `Skip`
- **Verdict:** `[DEEP DIVE]` or `[SKIP]`

## Quick Numbers
| Metric | Value | Source |
|:---|:---|:---|
| [Key metric 1] | [Value] | [Fig/Table] |
| [Key metric 2] | [Value] | [Fig/Table] |
```

### [DEEP DIVE] Template

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
| Claim | Evidence Quote | Location | Confidence |
|:---|:---|:---|:---|
| [claim1] | "[quote]" | [Section/¶] | ✅/⚠️/?/! |
| [claim2] | "[quote]" | [Section/¶] | ✅/⚠️/?/! |
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
- **Stated:** [Authors' own limitations]
- **Identified:** [Your critical observations]
- **Missing:** (!) [Critical gaps]

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

### Figures Analysis
| Figure | Title | Data | Insight |
|:---|:---|:---|:---|
| Fig N | [Title] | [Specific values] | [2-3 sentence analysis] |

### SWOT Analysis
| Dimension | Content |
|:---|:---|
| **Strengths** | [Why it works] |
| **Weaknesses** | [Methodological flaws/Data gaps] |
| **Opportunities** | [Potential follow-up experiments] |
| **Threats** | [Competitive technologies/Scalability] |

### Quantitative Benchmark Tables
#### Parameter-Outcome Matrix
| Variable 1 | Variable 2 | Outcome | Fit Type | R²/p-value |
|:---|:---|:---|:---|:---|
| [Value] | [Value] | [Outcome] | [Linear/etc] | [Value] |

#### Critical Thresholds
| Parameter | Lower Bound | Optimal Range | Upper Bound |
|:---|:---|:---|:---|
| [Parameter] | <[X] ineffective | [Y]-[Z] best | >[W] toxic |
  
#### Comparative Analysis vs Competitors
| Criterion | This Work | Competitor A | Competitor B | Winner |
|:---|:---|:---|:---|:---|
| [Metric1] | [Value] | [Value] | [Value] | ⭐ |


## Implementation & Transfer (Critical Thinking)
- **Transfer Difficulty Score:** [Metric1]: X/5 | [Metric2]: Y/5 | Overall Average: Z/5
  - Components that transfer directly: [List]
  - Components requiring re-optimization: [List]
  - Unknown variables: [List]
- **Complexity Score:** ⭐⭐⭐ (1=Facile, 5=Complex)
- **Chemical Route:** [Step-by-step Bench-Ready Protocol]
- **Cost/Scale:**[Price/Time, Budget/Timeline, Economic viability]
- **Kinetics Profile:** [Gelation speed, reversibility, or pH-responsiveness]
- **Biocompatibility:** High / Medium / Low / Not Mentioned
- **Lab Warning:** [Is there toxic reagent or extreme equipment required?]
- **Application and future direction:**

## Scholarly Mapping

### Identity Verification
- **DOI:** [DOI] ✅ Verified / (!) Not found
- **Citations:** [Total] | Trend: [↑/↓/→]
- **Venue Tier:** [Nature Index / Top-tier / Standard]

### Lab Genealogy
- **Lead Lab:** [Lab Name] — [Pioneer / Rising Star]
- **Institutional Influence:** [Core competency / Cross-domain]

### Academic Genealogy
| Tier | Paper | Contribution |
|:---|:---|:---|
| Foundational | [Author et al. (Year)] | [Established theory] |
| Direct Predecessor | [Author et al. (Year)] | [Provided A, lacked B] |
| This Work | Current paper | [Solves B] |

### Citation Sentiment
| Type | Proportion | Representative Citation |
|:---|:---|:---|
| Supporting | X% | [Citation] |
| Neutral | X% | [Citation] |
| Critical/Disputing | X% | (!) [Citation] |

### Strategic Positioning
- **Broken Ceiling:** [Specific bottleneck resolved]
- **Work Nature:** [Pioneering / Incremental / Application Transfer]

### Future Trajectory
| Timeframe | Predicted Direction |
|:---|:---|
| Short-term (T+2yr) | [Immediate extensions] |
| Long-term (T+10yr) | [Killer application] |
| New Research Avenues | [Sub-field opened] |

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
  
## ✅ Quality Checklist (Final)

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

```


---

