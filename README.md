# 🔍 Log Classification with Hybrid Framework

This project implements a **hybrid log classification system** that intelligently combines **regex rules**, **machine learning (ML)** via Sentence Transformers and Logistic Regression, and **LLMs (Large Language Models)** to classify log data of varying complexity and structure.


## 🚀 Key Features

- ✅ **Regex-based classification** for predictable patterns  
- 🤖 **ML-based classification** using BERT-style embeddings + Logistic Regression  
- 🧠 **LLM fallback support** for handling rare or unstructured log patterns  
- ⚡ **FastAPI-powered API** with endpoints for uploading and classifying log files  
- 📦 Modular design for easy integration and extensibility  


## 🧠 Classification Pipeline

### 1. **Regex Classifier**
- Handles simple, predictable patterns.
- Rule-based, fast, and efficient.

### 2. **Sentence Transformer + Logistic Regression**
- Trained on labeled logs.
- Handles moderately complex and contextual patterns.
- Uses `all-MiniLM-L6-v2` from [SentenceTransformers](https://www.sbert.net/).

### 3. **LLM Fallback (Optional)**
- For logs not confidently classified by the other methods.
- Useful in low-data or open-ended classification scenarios.


## 📁 Folder Structure

.
├── training/
│ ├── train_log_classifier.py # Training pipeline (SentenceTransformer + Logistic Regression)
│ ├── regex_classifier.py # Regex rule definitions
│ └── utils.py # Common utilities
├── models/
│ └── log_classifier.joblib # Trained Logistic Regression model
├── resources/
│ ├── test_logs.csv # Sample test logs
│ └── output_classified.csv # Output file with predicted labels
├── server.py # FastAPI app
├── requirements.txt # Python dependencies
└── README.md # This file


## ⚙️ Setup Instructions

### 1. Install Dependencies

Make sure you have Python 3.8+ installed. Then run:

```bash
pip install -r requirements.txt

## 🚀 Running the FastAPI Server

1. **Start the server**  
   ```bash
   uvicorn server:app --reload

Access the API

Main endpoint: http://127.0.0.1:8000/

Swagger UI: http://127.0.0.1:8000/docs

ReDoc: http://127.0.0.1:8000/redoc

## 📤 Usage

1. **Prepare your CSV**  
   Ensure your input file has the following columns:  

   | source   | log_message                             |
   |----------|-----------------------------------------|
   | serviceA | Server failed to respond to heartbeat   |
   | backendX | Multiple login attempts detected        |

2. **Upload via Swagger UI**  
   - Open [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)  
   - Select the **POST /classify/** endpoint  
   - Click **“Try it out”**, choose your CSV file, and click **Execute**

3. **Upload via `curl`**  
   ```bash
   curl -X POST "http://127.0.0.1:8000/classify/" \
        -F "file=@path/to/your/logs.csv" \
        -o classified_logs.csv


