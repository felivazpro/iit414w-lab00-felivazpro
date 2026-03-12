# PROMPTS.md — IIT414W · Lab 00

> **Note on this file:** The entries in this document were drafted with the assistance of GitHub Copilot. I provided the raw interaction details (original prompts, AI responses, and actions taken), and the AI helped structure them into the six-field format required by the AI Use Policy. All content reflects my actual interactions and decisions — the AI only assisted with formatting and phrasing.

---

## Interaction 1

**Tool:** Gemini  
**Notebook section:** 1 — Environment Verification

**1. Context**  
I was trying to run the full environment verification cell in `setup_check.ipynb` for the first time. The cell checks that all required packages are installed, sets up the FastF1 cache, and confirms that Git is available by calling `subprocess.run(['git', '--version'], ...)`. The cell raised a `FileNotFoundError` and I did not know the cause.

**2. Prompt(s)**  
> I ran the following environment check code and got a `FileNotFoundError: [WinError 2]` on the `subprocess.run(['git', '--version'], ...)` line. What could be causing this error?
>
> *(Pasted the full cell code and the traceback)*

**3. Relevant Output**  
Gemini explained that `FileNotFoundError: [WinError 2]` on Windows when using `subprocess.run` almost always means Python cannot find the executable being called — in this case `git`. It listed two possible causes: Git is not installed, or Git is not on the system PATH. It suggested running `git --version` in a normal terminal (CMD or PowerShell) to determine which case applied, and pointed to **git-scm.com** to download the installer if Git was missing. It also offered alternative fixes (`shell=True` and a `try/except` block) for PATH-related issues.

**4. Validation**  
Opened PowerShell and ran `git --version` — the command was not recognized, which confirmed that Git was simply not installed on the machine, not a PATH issue.

**5. Adaptations**  
Only the installation suggestion was used. The `shell=True` patch and `try/except` block proposed by the AI were not applied, as the original code already handled the case gracefully with `check=False` and a conditional print (`log.returncode == 0`).

**6. Final Decision**  
**Partially used.** Downloaded and installed Git from git-scm.com, restarted VS Code, and re-ran the notebook. The error was gone and no code changes were needed.

---

## Interaction 2

**Tool:** Gemini  
**Notebook section:** 5 — What Is Machine Learning?

**1. Context**  
I needed to understand the three main ML paradigms (supervised, unsupervised, and reinforcement learning) before working through Section 5 of the notebook. I also needed concrete Formula 1 examples for each paradigm — including what could go wrong if each one is misapplied — in order to complete the conceptual questions and the YOUR TURN cell.

**2. Prompt(s)**  
> Explain the following machine learning concepts in a clear and concise way: supervised learning, unsupervised learning, and reinforcement learning. For each one, provide a practical example applied to Formula 1 and describe the main risk if that paradigm is misapplied in that context.

**3. Relevant Output**  
Gemini provided a detailed explanation of each paradigm: what it is, how it works, when it is used, and what distinguishes it from the others. For each one it included multiple examples from different domains, then narrowed down to a specific Formula 1 scenario along with the main risk of misapplying that paradigm in that context.

**4. Validation**  
Cross-referenced the definitions and F1 examples against the taxonomy already present in the notebook (`setup_check.ipynb`, Section 5 — ML Taxonomy in F1 cell) to confirm they were consistent with the course framing.

**5. Adaptations**  
Used the explanations to build understanding before answering the "Before you code" questions. The F1 use cases and risks were adapted into my own wording when filling in the YOUR TURN table (`ml_f1_comparison` DataFrame).

**6. Final Decision**  
**Partially used.** The conceptual explanations were used as a reference to understand the material. The specific wording in the notebook and the code were written independently, informed by the AI's examples but not copied from them.

---

## Interaction 3

**Tool:** Gemini  
**Notebook section:** 2 — The Vibe Coder vs. Agentic Engineer (Reflection)

**1. Context**  
I needed to answer the reflection questions at the end of Section 2, which ask to explain the difference between a vibe coder and an agentic engineer, including a relatable analogy for a non-technical teammate. I wanted some examples or framings to help me think through the concept before writing my own answers.

**2. Prompt(s)**  
> Can you give me some analogies or examples that illustrate the difference between someone who codes based on intuition and blind trust in AI output (vibe coder) versus someone who validates every decision, checks assumptions, and documents their reasoning (agentic engineer)? I need something clear enough to explain to a non-technical person.

**3. Relevant Output**  
Gemini offered several analogies from different everyday contexts — cooking, construction, medicine — each showing two contrasting figures: one who acts on assumption and one who verifies at every step. It described the risks of each approach and why the verifying mindset leads to more reliable outcomes.

**4. Validation**  
The analogies were evaluated against the examples already in the notebook (Section 2 code snippets) to make sure they aligned with the course's framing of the spectrum.

**5. Adaptations**  
The cooking analogy resonated most and was adapted into the reflection answer: a cook who follows a recipe without tasting versus a chef who checks every ingredient and temperature.

**6. Final Decision**  
**Used.** The cooking analogy was considered well-constructed and directly applicable, so it was used in full as the basis for the non-technical explanation in the reflection.

---

## Interaction 4

**Tool:** Gemini  
**Notebook section:** 3 — Your First F1 Data Pull (Reflection)

**1. Context**  
I needed to answer the reflection questions at the end of Section 3, which ask to explain lap time consistency analysis in a way a non-technical teammate could understand. I wanted an analogy that captured the idea of comparing average performance versus consistency across multiple attempts.

**2. Prompt(s)**  
> Can you give me some analogies or examples that illustrate the difference between someone who performs very well once versus someone who performs consistently well across multiple attempts? I need something simple enough to explain to a non-technical person.

**3. Relevant Output**  
Gemini offered several analogies from everyday contexts — sports, delivery services, customer service — each contrasting a one-time top performer against a consistently reliable one. It explained why reliability is often more valuable than a single peak result.

**4. Validation**  
The analogies were checked against the actual results from the notebook cell (VER vs NOR standard deviation comparison) to make sure the framing matched what the data was showing.

**5. Adaptations**  
The delivery driver analogy resonated most with the context of the exercise and was adapted into the reflection answer as-is.

**6. Final Decision**  
**Used.** The analogy was considered a good fit for the concept and was used in full for the non-technical explanation in the reflection.

---

## Interaction 5

**Tool:** Gemini  
**Notebook section:** 4 — Prediction Card Activity

**1. Context**  
I needed to fill in the Prediction Card for the 2025 Drivers' Championship. The task required picking a predicted winner, listing data sources that would support that prediction, and identifying failure modes that could invalidate it. I was not fully familiar with the current driver lineup or which statistics would be most relevant to back a prediction.

**2. Prompt(s)**  
> Who are the drivers competing in the 2025 Formula 1 Drivers' Championship?

After reviewing the lineup and choosing Lando Norris as my predicted champion:

> I am predicting Lando Norris as the 2025 Drivers' Champion. What data or statistics would best support this prediction, and what are the most likely failure modes that could make it wrong?

**3. Relevant Output**  
Gemini listed the full 2025 driver lineup across all teams without ranking or recommending a winner. After independently selecting Norris, I followed up with a second prompt. Gemini then suggested relevant evidence such as win count from the previous season, lap time consistency, and car reliability data. For failure modes it mentioned on-track incidents, mechanical failures, and potential upgrades from rival teams closing the performance gap.

**4. Validation**  
Cross-checked the driver lineup against publicly available 2025 F1 season information to confirm it was accurate. Verified that the suggested evidence types (win record, lap time std, reliability) were measurable with the kind of data accessible through FastF1.

**5. Adaptations**  
The predicted champion (Norris) and the general categories of evidence and failure modes were kept. The specific wording was rewritten to match the notebook's format and my own reasoning.

**6. Final Decision**  
**Partially used.** The driver selection and evidence categories were adopted. The final text in the prediction card and the `prediction_card` dictionary were written independently.



