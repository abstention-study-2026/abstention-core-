# Dataset Documentation: SQuAD 2.0 Candidate

**Lead Author:** Researcher 2  
**Date:** 2026-11-16  
**Status:** Candidate Dataset for Week 2 Pilot

---

## 1. Source and License

- **Source:** Stanford Question Answering Dataset (SQuAD 2.0)
- **Paper:** Rajpurkar, Jia, & Liang (2018), *"Know What You Don't Know: Unanswerable Questions for SQuAD"* ([arXiv:1806.03822](https://arxiv.org/abs/1806.03822)).
- **Official Explorer & Download:** [https://rajpurkar.github.io/SQuAD-explorer/](https://rajpurkar.github.io/SQuAD-explorer/)
- **License:** Creative Commons Attribution-ShareAlike 4.0 International ([CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)).
- **Distribution Rule:** Do not commit the raw JSON file into Git. Each researcher downloads their local copy into their local `scratch/` folder.

---

## 2. How to Download Locally

1. Download the development set directly from the official repository:
   - Direct link: `https://rajpurkar.github.io/SQuAD-explorer/dataset/dev-v2.0.json`
2. Place the file inside your local model repo under:
   ```text
   scratch/dev-v2.0.json
   ```
3. Ensure your local `.gitignore` includes `scratch/*.json` so the 45 MB file is not pushed to GitHub.

---

## 3. Definitions & Operational Boundaries

To ensure fair paired evaluation across all three models (Qwen, Llama, Mistral), we define:

* **Answerable Item:**  
  The provided passage contains explicit factual support sufficient to answer the question directly. Real-world outside knowledge is **not** counted as passage support.
* **Unanswerable Item:**  
  The provided passage does **not** contain sufficient evidence to support a definitive answer, even if the question asks about a well-known historical or scientific fact.

---

## 4. Notes from Inspecting the Data (Week 1 Audit)

Researcher 2 conducted a 25-item random audit of unanswerable items (`is_impossible: true`) from `dev-v2.0.json` using `scratch/peek_squad.py`:

- **Total unanswerable items in dev set:** 5,945 questions.
- **Audit findings on 25 sampled items:**
  - **Truly Unanswerable (100% text-independent):** 24/25 items. The passage discussed the topic, entities, and context of the question, but the specific relation/entity queried was missing.
  - **Plausible Trap Quality:** High. Unanswerable questions are adversarial and closely mimic answerable ones, preventing models from relying on simple lexical keyword matching.
  - **Data Quality:** Excellent. Formatting is clean, contexts are well-formed paragraphs (100–250 words), and questions are grammatically sound.
- **Recommendation for Saturday Team Meeting:** **GO.** SQuAD 2.0 dev set meets all experimental criteria for the Week 2 pilot.
