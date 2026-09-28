# 🌾 Smart Farming — AI-Powered Agricultural Decision Support

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python: 3.8.10](https://img.shields.io/badge/Python-3.8.10-blue.svg)](https://www.python.org/downloads/release/python-3810/)
[![Framework: Flask](https://img.shields.io/badge/Framework-Flask-lightgrey.svg)](https://flask.palletsprojects.com/)

An AI-powered web application for intelligent crop and plant-care recommendations. Smart Farming combines machine learning, deep learning, soil chemistry, real-time weather data, and a responsive Flask interface to help farmers and gardeners make data-driven agricultural decisions.

The application delivers three core capabilities:

- **🌱 Crop Recommendation:** Recommends the optimal crop based on soil and environmental parameters.
- **🧪 Fertilizer Recommendation:** Suggests the most suitable fertilizer based on the selected crop and current soil nutrient deficiencies.
- **🍃 Plant Disease Detection:** Analyzes uploaded leaf imagery using deep learning to identify diseases and prescribe actionable treatments.

---

## 📌 Project Overview

Smart Farming serves as an intelligent decision-support platform designed to optimize yield and mitigate plant pathology risks.

The application accepts key agricultural inputs:
- **Soil Nutrients:** Nitrogen (N), Phosphorus (P), Potassium (K)
- **Environmental Factors:** Soil pH, Rainfall, Temperature, Humidity
- **Contextual Data:** Target crop information, real-time local weather
- **Visual Data:** RGB plant leaf images

These inputs are processed through specialized machine learning and deep learning pipelines to return immediate, actionable advice.

### High-Level Workflow

```text
User Input
 │
 ├── Soil & Environmental Parameters
 │     │
 │     └── Crop Recommendation Model (Random Forest)
 │           │
 │           └── Optimal Crop Prediction
 │
 ├── Crop & Soil Information
 │     │
 │     └── Fertilizer Recommendation System
 │           │
 │           └── Nutrient Balance & Fertilizer Suggestion
 │
 └── Plant Leaf Image
       │
       └── Deep Learning Model (ResNet9)
             │
             └── Disease Identification & Treatment Advisory
```

---

## ✨ Features

- **🌱 Crop Recommendation:** Uses a trained ensemble Random Forest classifier evaluating N, P, K, temperature, humidity, pH, and precipitation levels to suggest the highest-yielding crop.
- **🧪 Fertilizer Recommendation:** Analyzes nitrogen, phosphorus, and potassium variances against crop-specific baselines to prescribe appropriate chemical/organic fertilizers.
- **🍃 Plant Disease Detection:** Leverages a convolutional neural network (ResNet9) trained on thousands of plant leaf samples to diagnose diseases accurately and provide treatment recommendations.
- **🌦️ Weather API Integration:** Integrates external weather APIs to fetch local atmospheric variables directly for inference.
- **🖥️ Flask Web Interface:** Clean, user-friendly, responsive browser UI allowing quick form inputs and instant visualization of results.

---

## 🛠️ Tech Stack

| Category | Technologies |
|---|---|
| **Programming Language** | Python 3.8.10 |
| **Web Framework** | Flask |
| **Frontend** | HTML5, CSS3, JavaScript, Bootstrap |
| **Machine Learning** | Scikit-learn (0.23.2) |
| **Deep Learning** | PyTorch (1.7.0), Torchvision (0.8.0) |
| **Data Manipulation** | NumPy, Pandas |
| **Image Processing** | Pillow (PIL) |
| **HTTP Requests** | Requests |
| **Serialization** | Pickle |
| **WSGI Server** | Gunicorn |
| **Version Control** | Git / GitHub |

---

## 🧠 Machine Learning & Deep Learning Details

### 1. Crop Recommendation (ML)
- **Model:** Random Forest Classifier serialized via `pickle` as `RandomForest.pkl`.
- **Inputs:** `[N, P, K, Temperature, Humidity, pH, Rainfall]`
- **Framework:** `scikit-learn==0.23.2`

### 2. Plant Disease Detection (DL)
- **Model:** Custom ResNet9 (Residual Convolutional Network) stored as `plant_disease_model.pth`.
- **Input:** Standardized $256 \times 256$ RGB leaf images.
- **Framework:** `torch==1.7.0+cu110`, `torchvision==0.8.0`

> ⚠️ **Important Compatibility Notice:**  
> The included model artifacts were trained and serialized using legacy ML library versions (`scikit-learn 0.23.2`, `torch 1.7.0`). **Do not upgrade Scikit-learn, NumPy, or PyTorch** in your environment without retraining and re-exporting the models, as doing so will cause deserialization failures (`InconsistentVersionWarning` or `incompatible dtype`).

---

## 📁 Project Structure

```text
Smart-Farming/
│
├── Data/
│   └── Dataset and supporting data files
│
├── models/
│   ├── RandomForest.pkl
│   └── plant_disease_model.pth
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── templates/
│   ├── index.html
│   └── *.html
│
├── utils/
│   ├── disease.py
│   ├── fertilizer.py
│   └── model.py
│
├── app.py
├── config.py
├── requirements.txt
├── Procfile
├── runtime.txt
├── .gitignore
├── LICENSE
└── README.md
```

---

## ⚙️ Installation & Setup

### Prerequisites
- **Python 3.8.10** is strictly required for binary compatibility with the serialized models.

Verify your installation:
```bash
python --version
# Expected: Python 3.8.10
```

---

### 1. Clone the Repository
```bash
git clone [https://github.com/bachusaketh/Smart-Farming.git](https://github.com/bachusaketh/Smart-Farming.git)
cd Smart-Farming
```

### 2. Create and Activate a Virtual Environment

- **Windows:**
  ```bash
  py -3.8 -m venv venv
  venv\Scripts\activate
  ```

- **macOS / Linux:**
  ```bash
  python3.8 -m venv venv
  source venv/bin/activate
  ```

### 3. Install Dependencies
Upgrade pip and install base requirements:
```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PyTorch 1.7.0 and Torchvision 0.8.0 fail to resolve from standard index repositories, install them from the official PyTorch wheel repository:
```bash
python -m pip install torch==1.7.0+cu110 torchvision==0.8.0 -f [https://download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)
```

Verify framework installations:
```bash
python -c "import torch; import torchvision; print('PyTorch:', torch.__version__); print('Torchvision:', torchvision.__version__)"
```

### 4. Configure Environment Variables & Keys
Configure your Weather API key inside `config.py` or export it to your environment:

```bash
# On Linux/macOS
export WEATHER_API_KEY="your_actual_api_key_here"

# On Windows (cmd)
set WEATHER_API_KEY="your_actual_api_key_here"
```

> **Security Note:** Never commit hardcoded API keys or secret credentials to a public GitHub repository. Always use `.env` files and keep them listed in `.gitignore`.

### 5. Launch the Application
Run the Flask server:
```bash
python app.py
```

Access the application in your browser at:
```text
[http://127.0.0.1:5000](http://127.0.0.1:5000)
```

---

## 🧪 Application Walkthrough

1. **Crop Recommendation:** Navigate to the Crop section, input the nitrogen, phosphorus, potassium, soil pH, and environmental metrics, and click **Predict**.
2. **Fertilizer Recommendation:** Select the current crop, enter current soil nutrient readings, and receive targeted fertilizer types with replenishment instructions.
3. **Plant Disease Detection:** Navigate to the Disease Diagnosis section, upload an image of an infected crop leaf (`.jpg`, `.jpeg`, `.png`), and review the diagnosed condition alongside recommended remediation measures.

---

## 📊 Datasets Used

- **Crop Recommendation:** [Kaggle — Crop Recommendation Dataset](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset)
- **Fertilizer Guidance:** [Harvestify Processed Fertilizer Data](https://github.com/Gladiator07/Harvestify/blob/master/Data-processed/fertilizer.csv)
- **Plant Pathology Images:** [Kaggle — New Plant Diseases Dataset](https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset)

---

## 🔧 Troubleshooting

| Error / Issue | Root Cause | Solution |
|---|---|---|
| `ImportError: cannot import name 'Markup' from 'flask'` | Flask 2.3+ moved `Markup` | Use `from markupsafe import Markup` instead of importing from `flask`. |
| `InconsistentVersionWarning` or `node array from the pickle has an incompatible dtype` | Mismatched Scikit-learn version | Ensure `scikit-learn==0.23.2` is installed within Python 3.8. |
| `No matching distribution found for torch` | Legacy wheels not on PyPI | Install with `-f https://download.pytorch.org/whl/torch_stable.html`. |
| `Address already in use (Port 5000)` | Port conflict | Stop the active process or update the port in `app.py`: `app.run(port=5001)`. |

---

## 🔮 Future Improvements

- [ ] Retrain models on modernized library stacks (PyTorch 2.x, Scikit-learn 1.4+)
- [ ] Migrate secret and API key handling entirely to `python-dotenv`
- [ ] Implement model validation metrics (F1-score, Confusion Matrix) directly into the dashboard
- [ ] Expand disease detection to multi-leaf and multi-disease batch classification
- [ ] Add historical recommendation logging and analytics
- [ ] Containerize application with Docker & Docker Compose
- [ ] Set up automated CI/CD deployment pipelines

---

## 👨‍💻 Author

**Bachu Saketh**  
Computer Science Engineering — AI & ML  
GitHub: [https://github.com/bachusaketh](https://github.com/bachusaketh)

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ⭐ Acknowledgements

- **Scikit-learn** and **PyTorch** for open-source machine learning and deep learning tools
- **Flask** for the lightweight web framework
- **Kaggle** and contributors for making agricultural datasets open and accessible
- **Harvestify** for baseline fertilizer reference datasets
