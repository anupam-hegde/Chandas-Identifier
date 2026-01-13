# **Kannada Chandas Identifier (ಕನ್ನಡ ಛಂದಸ್ಸು)**

![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Flask-2.x-lightgrey?style=for-the-badge&logo=flask)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

> An AI-powered tool to analyze and identify the meter (Chandas) of Kannada poems.

<div align="center">
  <img width="900" alt="App Screenshot 1" src="https://github.com/user-attachments/assets/38c2e389-26f9-4911-992b-d93841efc2ea" />
  <br/><br/>
  <img width="900" alt="App Screenshot 2" src="https://github.com/user-attachments/assets/75ab558d-0277-4b02-b4a4-5532907080ba" />
</div>

<br/>

<div align="center">
  <a href="https://kannada-chandas-identifier-phase-1-1.onrender.com/">
    <img src="https://img.shields.io/badge/✨_Live_Demo-Click_Here-FF4B4B?style=for-the-badge&logo=appveyor" height="40" />
  </a>
</div>

---

## **🚀 Features**

Unlock the beauty of Kannada literature with these powerful features:

*   **🔍 Precision Meter Identification**: Detects complex Laghu/Guru patterns and Matra counts to identify meters like **Kanda Padya**, **Shatpadi** (Bhamini/Vardhaka), and various **Vruttas** (Utpalamala, Champakamala, etc.).
*   **📷 OCR Capability**: Upload images of poems! The integrated Tesseract OCR automatically extracts text for analysis.
*   **📝 Multi-Stanza Support**: Paste entire poems; the tool intelligently separates and analyzes each stanza individually.
*   **💾 Auto-Save History**: Your analyzes are precious. Valid results are automatically saved to a local SQLite database (`chandas.db`) for easy retrieval.
*   **📄 PDF Reports**: Generate and download professional PDF reports of your analysis.
*   **📊 Visual Scansion**: See the poem's skeleton with a clear line-by-line breakdown of Laghu (U) and Guru (-) markers.

---

## **🏗️ Tech Stack**

This project is built using a robust and modern technology stack:

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Backend** | ![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white) ![Flask](https://img.shields.io/badge/-Flask-000000?logo=flask&logoColor=white) | Core logic and API handling. |
| **Frontend** | ![HTML5](https://img.shields.io/badge/-HTML5-E34F26?logo=html5&logoColor=white) ![TailwindCSS](https://img.shields.io/badge/-TailwindCSS-38B2AC?logo=tailwind-css&logoColor=white) | Responsive and beautiful user interface. |
| **OCR Engine** | ![Tesseract](https://img.shields.io/badge/-Tesseract-blue) | Optical Character Recognition for image inputs. |
| **Database** | ![SQLite](https://img.shields.io/badge/-SQLite-003B57?logo=sqlite&logoColor=white) | Lightweight local storage for analysis history. |
| **Image Processing** | ![Pillow](https://img.shields.io/badge/-Pillow-green) | Image manipulation for OCR preprocessing. |

---

## **🏛️ Architecture**

### **System Flow**

The application follows a clean client-server architecture.

```mermaid
graph TD
    A[User] -->|Input Text/Image| B(Frontend UI)
    B -->|API Request /analyze or /ocr| C{Flask Backend}
    C -->|Image Upload| D[Tesseract OCR]
    D -->|Extracted Text| C
    C -->|Text Input| E[KannadaChandasIdentifier Class]
    E -->|1. Clean Text| E1[Preprocessor]
    E1 -->|2. Calc Laghu/Guru| E2[Pattern Engines]
    E2 -->|3. Match Ganas| E3[Meter Classifier]
    E3 -->|Analysis Result| C
    C -->|Save Valid Result| F[(SQLite Database)]
    C -->|JSON Response| B
    B -->|Display Results| A
```

### **Core Algorithm (`KannadaChandasIdentifier`)**

The heart of the application lies in the `KannadaChandasIdentifier` class in `app.py`. Here's how it works:

1.  **Text Cleaning**: Removes non-Kannada characters (except spaces) to ensure noise-free analysis.
2.  **Laghu/Guru Assignment**: 
    *   Iterates through characters.
    *   Assigns **Guru (-)** for long vowels, specific consonant clusters (Vattakshara), and Yogavahas (Anusvara/Visarga).
    *   Assigns **Laghu (U)** for short vowels.
3.  **Gana Grouping**: Groups the Laghu/Guru sequence into triplets (Ganas) like 'Ma', 'Ya', 'Ra', etc.
4.  **Pattern Matching**:
    *   **Vruttas**: Checks for specific Gana sequences (e.g., *Utpalamala* matches `Bha-Ra-Na-Bha-Bha-Ra-La-Ga`).
    *   **Matra Meters**: Calculates total Matras (time units) per line to identify **Kanda Padya** or **Shatpadi**.

---

## **📂 Project Structure**

```
Kannada_Chandas_Identifier_phase_1/
├── app.py                # 🧠 Main Flask application & Logic
├── index.html            # 🎨 Frontend UI (HTML/JS/Tailwind)
├── requirements.txt      # 📦 Python Dependencies
├── dockerfile            # 🐳 Docker configuration
├── chandas.db            # 🗄️ SQLite Database (Auto-generated)
├── favicon.png           # 🖼️ Icon assets
└── README.md             # 📖 Documentation
```

---

## **🛠️ Installation**

### **Prerequisites**
1.  **Python 3.x** installed.
2.  **Tesseract OCR** installed (Critical for image features).

### **Step 1: Install Tesseract OCR**
This is required for the image scanning feature.

*   **Windows**: 
    *   Download from [UB-Mannheim/tesseract](https://github.com/UB-Mannheim/tesseract/wiki).
    *   **Crucial**: Select **"Kannada"** scripts during installation.
    *   Reference path: `D:\tessaract\tesseract.exe` (Update in `app.py` if different).
*   **Linux**: `sudo apt install tesseract-ocr tesseract-ocr-kan`
*   **Mac**: `brew install tesseract-lang`

### **Step 2: Setup Project**
```bash
# 1. Clone the repository
git clone https://github.com/yourusername/Kannada_Chandas_Identifier.git
cd Kannada_Chandas_Identifier

# 2. Install dependencies
pip install -r requirements.txt
```

### **Step 3: Run the App**
```bash
python app.py
```
> You should see: `SUCCESS! Server is running on http://127.0.0.1:5000`

---

## **📖 Usage Guide**

1.  **Analyze Text**: Type/Paste your poem in the main text box. Click **Analyze**.
2.  **Scan Image**: Toggle to the Image tab (if available) or use the "Scan Image" button. Upload a `.png` or `.jpg`.
3.  **View Results**: The result cards will show the meter, ganas, and line-by-line breakdown.
4.  **History**: Click the **History** icon to revisit past analysis.

---

## **❓ Troubleshooting**

| Issue | Solution |
| :--- | :--- |
| **Tesseract Not Found** | Ensure Tesseract is installed and the path in `app.py` matches your system path. |
| **OCR Errors** | Make sure you installed the **Kannada** language pack for Tesseract. |
| **Server Error** | check your terminal for Python tracebacks. Ensure all dependencies are installed. |

---

<div align="center">
  <i>Made with ❤️ for Kannada Literature</i>
</div>
