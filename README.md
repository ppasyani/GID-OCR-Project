# GID-OCR-to-Spreadsheet-Project

This notebook trains and evaluates a **spaCy Named Entity Recognition (NER)** model to convert  
noisy OCR-style receipt text into structured tabular data with the following fields:

- **time**  
- **product**  
- **quantity**  
- **price_per_pax**  
- **total_price**   

The workflow supports both **synthetic datasets** and **real OCR exports**, normalizes the text into a consistent schema, trains an NER model, evaluates accuracy, and finally produces a clean spreadsheet (CSV/XLSX).  

---

## 📑 Notebook Sections

1. **Setup**  
   Install dependencies, set up folders, and configure paths.

2. **Dataset (Synthetic or OCR)**  

   <details>
   <summary>🔹 Option 1 — Synthetic Receipts</summary>

   Run this if you want to **simulate OCR data** by generating a dummy dataset (`receipts_dummy_en.csv / .xlsx`).  
   Useful for experimenting or if no OCR output is available yet.  

   </details>

   <details>
   <summary>🔹 Option 2A — OCR Upload + Normalize</summary>

   Run this if you already have an **OCR export file (CSV/XLSX)** with a `raw_text` column.  
   You will upload the file directly from your computer into Colab.  

   ⚠️ Make sure to run the **OCR Normalization Helpers** cell first, since it defines the regex and parsing functions used here.

   </details>

   <details>
   <summary>🔹 Option 2B — OCR from Google Drive + Normalize</summary>

   Run this if your OCR files are already stored in a Google Drive folder.  
   This option supports multiple CSV/XLSX files at once.  

   ⚠️ Make sure to run the **OCR Normalization Helpers** cell first, since it defines the regex and parsing functions used here.

   </details>

3. **Preprocessing → NER Training Examples**  
   Align entity spans (`TIME`, `PRODUCT`, `QTY`, `PRICE_UNIT`, `PRICE_TOTAL`) and handle OCR noise.  

4. **Train/Validation Split**  
   Split annotated examples into training and dev sets.  

5. **Model Training (spaCy NER)**  
   Train and save the model (`last` and `best` checkpoints).  

6. **Evaluation**  
   - Entity-level metrics: Precision / Recall / F1  
   - Spreadsheet-style metrics: per-field accuracy & strict row accuracy  

7. **Inference → Structured Spreadsheet**  
   Apply the model to new receipts, export structured results to **CSV/XLSX** (either in Colab or directly to Google Drive).  

8. **(Optional) Post-processing**  
   Regex fallbacks, math-based repairs (`qty * unit = total`), and product lexicon matching.  

---

> 💡 **Tip:** Do not run both **Option 1** and **Option 2** at the same time. Pick one source, prepare the dataset, then continue to next step
