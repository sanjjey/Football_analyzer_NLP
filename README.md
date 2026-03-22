# ⚽ Football Commentary Analyzer Pipeline

An end-to-end, AI-powered pipeline that transforms football (soccer) commentary transcripts into structured game analytics, sentiment scores, and automated pitch heatmaps.

## 📖 Overview
This project processes unstructured **ASR (Automatic Speech Recognition)** commentary logs to extract deep match insights. By leveraging the high-speed inference of the **Groq API (Llama-3.3-70b)**, the pipeline analyzes time-stamped text to deduce game flow, validates AI logic through a custom verification engine, and visualizes team dominance using `mplsoccer`.

---

## 🗂 Dataset: SoccerNet-Echoes
The pipeline utilizes transcript files (`1_asr.json` and `2_asr.json`) sourced from the **SoccerNet-Echoes** dataset.
* **Content:** Time-stamped text of live commentator speech.
* **Processing:** The pipeline segments these transcripts into dynamic time intervals to analyze the match chronologically.

---

## ✨ Key Features
* **LLM-Powered Insights:** Employs Llama-3.3-70b to interpret nuance in commentary, identifying possession shifts, match sentiment, and key events (shots, fouls, goals).
* **Automated Heatmaps:** Translates possession and action data into spatial pitch visualizations using `mplsoccer`.
* **Data Verification Engine:** A robust `DataVerifier` class acts as a guardrail, cross-checking LLM outputs for mathematical consistency (e.g., ensuring total possession equals 100%) and logical soundness.
* **Structured Logging:** Generates a clean Pandas DataFrame of the match timeline and a `verification_log.csv` to track AI accuracy.

---

## 🧠 Pipeline Architecture

1.  **Data Ingestion:** Loads JSON transcripts and segments them by match minute/segment.
2.  **Analysis (Groq LLM):** Prompts the LLM to extract possession metrics and sentiment from the text.
3.  **Verification:** Validates the output to eliminate hallucinations and ensure data integrity.
4.  **Visualization:** Generates heatmaps representing "Home" vs "Away" dominance for each segment.
5.  **Reporting:** Compiles the validated data into a final tabular dataset.

---

## 🛠 Prerequisites & Installation

Ensure you have Python 3.8+ installed. You can install the required dependencies via pip:

```bash
pip install mplsoccer groq pandas matplotlib
