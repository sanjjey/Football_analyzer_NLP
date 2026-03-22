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

## 🧠 NLP & LLM Contributions

The core intelligence of this pipeline relies on Advanced Natural Language Processing (NLP) to bridge the gap between spoken commentary and structured data.

### 1. Semantic Context Extraction
Unlike simple keyword matching, the NLP engine understands the **context** of football phrases. 
* *Example:* It distinguishes between "finding the net" (a goal) and "hitting the side netting" (a miss), which traditional parsers might confuse.

### 2. Entity & Event Recognition
The pipeline performs **Named Entity Recognition (NER)** on the fly to identify:
* **Players & Teams:** Mapping names mentioned in ASR to the active squads.
* **Spatial Indicators:** Extracting phrases like "down the left wing" or "inside the box" to provide coordinates for heatmap generation.

### 3. Sentiment & Intensity Analysis
Using the **Llama-3.3-70b** model via Groq, the system performs a dual-layer sentiment analysis:
* **Match Tone:** Is the game "stagnant," "end-to-end," or "aggressive"?
* **Crowd/Commentator Bias:** Detecting shifts in excitement levels to identify "High-Pressure" moments automatically.

### 4. Sentiment Extraction (VADER-NLP)
The crowd intensity, the momentum flow and the total sentiment score is analyzed using a NLP based lexicon based model called VADER which calculates the sentiments separately and generates the score according to the particular segment of time.

### 5. Temporal Reasoning (Time-Series NLP)
The pipeline synchronizes disjointed ASR chunks into a linear narrative. It uses **Temporal Reasoning** to decide if a possession started in one text segment and concluded in another, ensuring the 100% possession logic holds true across timestamps.

---

## ✨ Key Features
* **LLM-Powered Insights:** Uses Large Language Models to read commentary and deduce which team holds possession, the sentiment of the match, and key events (shots, fouls, goals).
* **Automated Heatmaps:** Translates NLP-extracted spatial data into density visualizations using `mplsoccer`.
* **Data Verification Engine:** Includes a robust `DataVerifier` class that acts as a guardrail. It cross-checks the LLM's output for mathematical consistency and logical soundness.
* **Structured Logging:** Outputs a clean Pandas DataFrame of the match timeline and a `verification_log.csv` detailing the AI's accuracy and consistency.
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
