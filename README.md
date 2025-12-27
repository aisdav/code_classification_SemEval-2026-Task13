# SemEval-2026 Task 13: Detecting Machine-Generated Code (Task A)

This is a **pet project** for learning purposes.  
I do not aim for the best score; the goal is to gain experience.  
I **did not use transformers** like BERT or UniXcoder yet, but in the future, I plan to explore neural network approaches.  

The evaluation metric for this task is **Macro F1**.  
Note: for unseen languages, generator families, and code application scenarios, this solution may not perform well due to scaling and time constraints.  
I used a **small subset of the real dataset from GitHub (~10k samples)** for experimentation.

**Official Task and Dataset:** [SemEval-2026 Task 13 GitHub](https://github.com/mbzuai-nlp/SemEval-2026-Task13/tree/main)

---

## 1. Exploratory Data Analysis (EDA)

- The dataset is **balanced** between human-written and AI-generated code.  
- Code is written in **3 languages**: Python, Java, C++.  
- There are **61 different generator models**.  
- Most **very long codes (90%) were AI-generated**.  
- New numeric features were added:
  - `length` – length of code in characters  
  - `strings_number` – number of lines  
  - `comments_number` – number of comments  
  - `density_of_string` – ratio of non-whitespace characters  
  - `length_to_comms` – length divided by number of comments  

---

## 2. Model Experiments

1. **Baseline models (numeric features only):**  
   - Logistic Regression → **Macro F1 = 0.67**  
   - Random Forest → **Macro F1 = 0.73**  
   - XGBoost → **Macro F1 = 0.70**  
   - Attempts to optimize Random Forest did not significantly improve results.

2. **Character n-grams + Logistic Regression:**  
   - Added **character n-grams (4–6 chars)** with TF-IDF  
   - Captured coding style patterns effectively  
   - Resulted in **Macro F1 = 0.865** — a significant improvement

3. **Hybrid / Ensemble approach:**  
   - Combined **Random Forest on numeric features** + **char n-gram Logistic Regression**  
   - Provided minor improvements but valuable in hybrid pipeline

---

## 3. Deployment

- Initial **Streamlit deployment** was unstable.  
- Created a **hybrid pipeline** that accepts both numeric features and n-grams.  
- The model now works reliably and can predict new code snippets.

---

## 4. Next Steps

- Explore **neural network approaches** (CodeBERT, UniXcoder).  
- Scale to **full dataset** for better performance.  
- Experiment with **token-level n-grams** or embeddings to reduce style bias.

---

## Notes

- This project is meant for **learning and experimentation**, not leaderboard-level submission.  
- The **biggest improvement** came from capturing style patterns via **character n-grams**.
