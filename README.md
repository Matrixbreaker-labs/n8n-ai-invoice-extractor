# 🤖 AI-Powered PDF Invoice Extractor (n8n + Google Gemini + Google Sheets)

An automated, zero-manual-entry workflow built with **n8n** and **Google Gemini AI** that extracts structured financial data from unstructured PDF supplier invoices (both digital and scanned) and logs the clean output directly into **Google Sheets**.

## 🏗️ Workflow Architecture

The pipeline operates across four automated nodes:
1. **Upload Invoice PDF (Form Trigger):** Provides a clean web form interface to upload supplier invoices in PDF format.
2. **Extract Invoice Data (Google Gemini AI):** Uses Gemini's native document analysis capabilities to read the PDF and extract key financial fields without fragile Regex rules.
3. **Parse Extracted Fields (Data Normalizer):** Enforces strict formatting (normalizing dates to `YYYY-MM-DD` and amounts to clean numeric values) and timestamps the execution.
4. **Save to Google Sheets (Database Storage):** Automatically appends a new structured row into the target `AI_Invoices_DB` spreadsheet.

## ✨ Key Features
* **Layout-Agnostic Parsing:** Handles varying invoice templates from multiple suppliers effortlessly.
* **Scanned & Digital PDF Support:** Reads both selectable text PDFs and image-based scanned documents.
* **Zero Hallucination Constraints:** Configured to return `null` or blank fields rather than guessing if data is missing.
* **Plug-and-Play Deployment:** Ready to import into any n8n Cloud or Self-Hosted instance via the included `.json` file.

## 📊 Extracted Data Schema

| Column Name | Data Type | Description | Example Output |
| :--- | :--- | :--- | :--- |
| **Supplier Name** | String | Formal name of the vendor | `Meghna Office Supplies Ltd.` |
| **Invoice Number** | String | Unique invoice reference ID | `INV-2026-04817` |
| **Invoice Date** | Date (`YYYY-MM-DD`) | Standardized issue date | `2026-11-03` |
| **Total Amount** | Float | Total billed amount | `3300.00` |
| **Currency** | String | ISO currency code | `USD` / `BDT` |
| **Processed At** | Timestamp | Automated execution log time | `2026-11-10T21:55:00Z` |

## 🚀 How to Import & Run

1. Download the `PDF Invoice Extractor (Gemini → Google Sheets).json` file from this repository.
2. Open your **n8n** dashboard (Cloud or Self-Hosted) and click **Create Workflow**.
3. Click the top-right menu (`...`) and select **Import from File**, then choose the downloaded `.json` file.
4. Connect your **Google Gemini API** credential and **Google Sheets** account.
5. Create a Google Sheet named `AI_Invoices_DB` with the headers listed in the schema table above, map the columns, and click **Execute** or **Publish**.

---
*Architected by Md Jahangir Alam | AI Automation & Data Engineer*
