# Dual Role of LLMs in Advanced Mathematical Problem Solving

This repository accompanies a study on how Large Language Models (LLMs) — specifically the web version of ChatGPT 5.1 — behave when asked to tackle a genuine open problem in graph theory.

The project investigates both **helpful** and **harmful** aspects of LLM assistance. In particular, it examines how the model:

- supports **orientation, brainstorming, and strategy formation**, and  
- fails at **deep logical reasoning and proof construction**.

The experiments focus on the following unsolved problem in graceful graph labeling:

> **Problem.** If \(G\) is nongraceful, is the line graph \(L(G)\) graceful?

LLM interactions were conducted entirely through the **ChatGPT 5.1 web interface**, using uploaded PDFs and text prompts. This setup is intended to mirror how students and researchers actually use LLMs in practice.

---

## Repository Structure

```text
.
├── prompts/
│   ├── prompt_1/
│   │   ├── llm_output.txt
│   │   ├── prompt.txt
│   │   └── what_to_analyze.txt
│   ├── prompt_2/
│   │   ├── llm_output.txt
│   │   ├── prompt.txt
│   │   └── what_to_analyze.txt
│   ├── prompt_3/
│   ├── prompt_4/
│   ├── prompt_5/
│   ├── prompt_6/
│   ├── prompt_7/
│   └── prompt_8/
├── A Dynamic Survey of Graph Labeling.pdf
└── On Graceful Line Graphs.pdf
```

### `prompts/` directory

Each `prompt_k/` folder (for \(k = 1, \dots, 8\)) corresponds to one experimental interaction with the LLM.

Inside each folder:

- **`prompt.txt`**  
  The exact text given to ChatGPT 5.1 in that experiment.

- **`llm_output.txt`**  
  The verbatim model response for that prompt (including all visible output in the web UI).

- **`what_to_analyze.txt`**  
  A short description of what aspects of the LLM’s response are analyzed for that prompt (e.g., correctness of definitions, hallucinated theorems, logical gaps, etc.).

### Problem background PDFs

- **`A Dynamic Survey of Graph Labeling.pdf`**  
- **`On Graceful Line Graphs.pdf`**

These two papers provide the mathematical background for line graphs, graceful labelings, and related results. They were uploaded to ChatGPT 5.1 as context **only for Prompt 1**. All subsequent prompts build on the model’s internal understanding developed from that initial interaction.

---

## Experimental Design

The experiment consists of eight prompts, grouped into phases that mirror natural stages of mathematical inquiry:

1. **Orientation and Conceptual Understanding**  
2. **Brainstorming and Related Areas**  
3. **Literature and Theorem Recall (Hallucination Stress Test)**  
4. **Strategy Formation**  
5. **Proof Attempts and Deep Reasoning**  
6. **Self-Evaluation and Correction**

Each prompt is described below along with what is analyzed in the corresponding LLM output.

---

## Prompt-by-Prompt Description

### Prompt 1 — Understanding the Problem

**File:** `prompts/prompt_1/`

**Prompt summary (`prompt.txt`):**

- The LLM is given the open problem  
  > *If \(G\) is nongraceful then \(L(G)\) is graceful?*  
- Two PDFs are provided as input:  
  `A Dynamic Survey of Graph Labeling.pdf` and `On Graceful Line Graphs.pdf`.  
- The model is asked to:
  1. Restate the main problem in its own words.  
  2. List key definitions and properties.  
  3. Explain why the problem is challenging/interesting.  
  4. Identify natural simplifications or special cases.

**What is analyzed (`what_to_analyze.txt`):**

1. Correctness of definitions.  
2. Faithfulness of the problem restatement.  
3. Ability to identify important structural components of the problem.

---

### Prompt 2 — Brainstorming Approaches

**File:** `prompts/prompt_2/`

**Prompt summary:**

- The LLM is asked to brainstorm **6–10 possible approaches or ideas** a researcher might explore, and for each:
  1. Describe the core insight.  
  2. Explain why it might be promising.  
  3. Point out potential obstacles.

**What is analyzed:**

1. The LLM’s ability to generate conceptual ideas.  
2. Presence of reasonable themes (e.g., parity, degrees, line-graph structure).

---

### Prompt 3 — Related Areas of Graph Theory

**File:** `prompts/prompt_3/`

**Prompt summary:**

- The model is asked to identify **areas of graph theory/graph labeling** most closely related to the problem, and for each:
  1. Name the area.  
  2. Explain how it relates to the problem.  
  3. Mention relevant concepts or tools.

**What is analyzed:**

1. Whether the suggested topics are actually relevant.  
2. Whether the explanations are sensible and consistent with known theory.

---

### Prompt 4 — Theorem and Conjecture Recall (Hallucination Test)

**File:** `prompts/prompt_4/`

**Prompt summary:**

- The LLM is asked to list **8–12 theorems, known results, or named conjectures** directly relevant to the problem, and for each:
  1. Provide the name of the result.  
  2. State the authors (if known).  
  3. Provide a brief summary.  
  4. Indicate whether it is unsure.

- The prompt explicitly instructs the model **not to invent results or authors**.

**What is analyzed:**

Each item is categorized as:

1. Real (matches actual literature).  
2. Approximate / mixed (partially correct but inaccurate or conflated).  
3. Invented / hallucinated (no basis in the literature).

This prompt is used to study **academic hallucinations** and the reliability of LLM-generated references.

---

### Prompt 5 — High-Level Strategies

**File:** `prompts/prompt_5/`

**Prompt summary:**

- The LLM is asked to propose **3–5 distinct high-level strategies** to resolve the problem. For each strategy:
  1. Explain the core idea.  
  2. List any structural lemmas that might be needed.  
  3. Predict the hardest obstacle to success.

**What is analyzed:**

1. Coherence of the proposed strategies.  
2. Usefulness of the decomposition into subproblems and lemmas.

---

### Prompt 6 — Full Proof Attempt

**File:** `prompts/prompt_6/`

**Prompt summary:**

- The LLM is asked to attempt a **full, rigorous proof** of the main conjecture, written as if for a mathematics journal:
  - State lemmas clearly.  
  - Justify each inference.  
  - Avoid vague reasoning.

**What is analyzed:**

1. Logical gaps and missing justifications.  
2. Invented lemmas or results.  
3. Incorrect identities or structural claims.  
4. Contradictions and circular reasoning.  
5. False generalizations and unjustified conclusions.

This prompt is central for assessing **deep reasoning failures**.

---

### Prompt 7 — Self-Critique of the Proof

**File:** `prompts/prompt_7/`

**Prompt summary:**

- The LLM is asked to **re-read its own proof** from Prompt 6 and:
  1. Identify steps that may be incorrect, incomplete, or unjustified.  
  2. Explain why each is problematic.  
  3. Attempt to repair or clarify the questionable parts.

**What is analyzed:**

- Whether the LLM:
  1. Defends incorrect steps instead of correcting them.  
  2. Only rephrases arguments without fixing the underlying logic.  
  3. Fails to detect contradictions or serious flaws.  
- Also checked: whether it **actually finds any genuine issues** in its own reasoning.

---

### Prompt 8 — Revised Proof After Self-Critique

**File:** `prompts/prompt_8/`

**Prompt summary:**

- After the self-critique, the LLM is asked to:
  > “Correct the identified flaws and provide a final rigorous proof for the problem without any flaws.”

**What is analyzed:**

1. Whether the LLM meaningfully corrects previously identified mistakes.  
2. Whether the revised proof improves over the original from Prompt 6.  
3. Whether the final proof truly resolves the original problem.

---

## How to Use This Repository

Reviewers and readers can:

1. **Inspect `prompt.txt`** in each `prompt_k/` folder to see the exact instructions given to the LLM.  
2. **Read `llm_output.txt`** to examine the model’s verbatim response.  
3. **Consult `what_to_analyze.txt`** for a concise description of what aspects of the response are examined in the paper.  
4. **Reference the two PDFs** to understand the mathematical background that the LLM had access to for Prompt 1.

This structure is intended to make the experimental setup transparent and reproducible, and to allow others to evaluate both the **strengths** (orientation, brainstorming, strategy) and **weaknesses** (hallucinations, flawed proofs, poor self-correction) of LLMs in this context.
