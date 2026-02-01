<table border="0" cellspacing="0" cellpadding="0" width="100%">
<tr>
<td width="65%" align="center" valign="middle">
<img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/project.png"
     width="100%"
     style="height:auto; max-height:500px; border-radius:8px;"
     alt="Hallucination Detection Architecture">
</td>

<td width="35%" valign="top" style="padding-left: 20px;">
<h3>🔍 LLM Hallucination Evaluators</h3>

<p><strong>Stack:</strong><br>
<code>Python</code> · <code>Guidance</code> · <code>PyTorch</code> · <code>Transformers</code> · <code>Jupyter</code>
</p>

<p><strong>Description:</strong><br>
A research project for the <b>ELOQUENT Lab @ CLEF 2024</b>. This system utilizes LLMs as autonomous evaluators to generate and detect hallucinations in <b>Machine Translation</b> and <b>Paraphrasing</b> across multiple languages.
</p>

<p><strong>Highlights:</strong><br>
Implemented <b>Ensemble Majority Voting</b> and <b>Inverse Proportion Weighting</b> to optimize detection accuracy across Llama 3, Gemma, GPT-3.5 Turbo, and GPT-4 architectures.
</p>

<p>
<a href="https://arxiv.org/abs/2407.09152">📰 Read Paper (arXiv)</a><br>
</p>
</td>
</tr>
</table>

<table border="0" cellspacing="0" cellpadding="0" width="100%">
<tr>
<td width="33%" align="center" style="padding:5px;">
<img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/task_builder.png" width="100%" style="border-radius:6px;" alt="Builder Task Workflow">
</td>
<td width="33%" align="center" style="padding:5px;">
<img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/voting.png" width="100%" style="border-radius:6px;" alt="Ensemble Methods">
</td>
<td width="33%" align="center" style="padding:5px;">
<img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/detection_task.png" width="100%" style="border-radius:6px;" alt="Performance Metrics">
</td>
</tr>
</table>

---

## Abstract
Hallucination detection in Large Language Models (LLMs) is crucial for ensuring their reliability. This work presents our participation in the CLEF ELOQUENT HalluciGen shared task, where the goal is to develop evaluators for both generating and detecting hallucinated content. We explored the capabilities of four LLMs: **Llama 3, Gemma, GPT-3.5 Turbo, and GPT-4**, for this purpose. We also employed ensemble majority voting to incorporate all four models for the detection task. The results provide valuable insights into the strengths and weaknesses of these LLMs in handling hallucination generation and detection tasks.

## Implementation & Methodology

This project was divided into two primary phases as part of the **ELOQUENT Lab 2024 HalluciGen task**: the Builder task and the Breaker task.

### 1. Hallucination Generation (Builder Task)
We developed evaluators to produce "hallucination-aware" models across two scenarios: **Machine Translation** (DE-EN, EN-DE, FR-EN, EN-FR) and **Paraphrase Generation** (English, Swedish).

<p align="center">
  <img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/hallucination_generation.png" width="80%" alt="Hallucination Generation Pipeline">
</p>

* **Objective:** Given a source sentence, the model generates two hypotheses: one correct translation/paraphrase and one hallucinated version.
* **Structured Control:** We utilized the **Guidance framework** to enforce JSON formatting and implement **Chain-of-Thought (CoT)** prompting.

### 2. Hallucination Detection
We evaluated how effectively LLMs can identify factual errors in both human and machine-generated contexts.

<p align="center">
  <img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/detection_task.png" width="80%" alt="Detection Step Overview">
</p>

* **Ensemble Voting:** A **Majority Voting** approach was used to combine the outputs of Llama 3, Gemma, GPT-3.5, and GPT-4 to act as a single robust classifier.
* **Inverse Proportion Weighting:** To improve accuracy, we calculated weights based on the inverse of each model's F1-score from the validation set, assigning higher influence to top-performing models.
* **Prompt Engineering:** We tested four types of prompts, ranging from simple binary labels to complex descriptions containing formal definitions and few-shot examples.

### 3. Task-Specific Workflows

<table border="0" cellspacing="0" cellpadding="0" width="100%">
<tr>
<td width="50%" align="center" style="padding:10px;">
  <img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/translation_task.png" width="100%" alt="Translation Task">
  <p><i>Machine Translation Evaluation</i></p>
</td>
<td width="50%" align="center" style="padding:10px;">
  <img src="https://raw.githubusercontent.com/nat-hu/eloquent-hallucination-lab/main/images/paraphrase_task.png" width="100%" alt="Paraphrase Task">
  <p><i>Paraphrase Generation Evaluation</i></p>
</td>
</tr>
</table>

### 4. Key Findings
* **Top Performance:** GPT-4 achieved a peak **0.91 F1-score** on English paraphrasing tasks.
* **Model Biases:** Llama 3 exhibited notable **gender bias**, failing to recognize feminine nouns (e.g., *Wirtschaftsprüferin*) and incorrectly labeling accurate translations as hallucinations based on gender assumptions.
* **Technical Hurdles:** Models generally struggled with measurement conversions (e.g., meters to kilometers) and diverse date formats.

---
*Research conducted by Anh Thu Maria Bui, Saskia Felizitas Brecht, Natalie Hußfeldt, Tobias Jennert, Melanie Ullrich at **TH Köln - University of Applied Sciences**.*
