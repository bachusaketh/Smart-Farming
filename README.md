Smart Farming 🌾

An AI-powered web application for intelligent crop and plant-care recommendations. Smart Farming combines machine learning, deep learning, soil parameters, weather information, and a Flask web interface to help users make data-driven agricultural decisions.

The application currently provides three core capabilities:

🌱 Crop Recommendation — recommends a suitable crop based on soil and environmental parameters.

🧪 Fertilizer Recommendation — suggests an appropriate fertilizer based on the selected crop and soil conditions.

🍃 Plant Disease Detection — analyzes an uploaded plant-leaf image using a deep learning model and provides disease information and recommended treatment guidance.

📌 Project Overview

Smart Farming is a machine-learning and deep-learning based agricultural decision-support application built with Python and Flask.

The system accepts agricultural inputs such as:

Nitrogen (N)

Phosphorus (P)

Potassium (K)

Soil pH

Rainfall

Temperature

Humidity

Crop information

Plant-leaf images

These inputs are processed by trained machine-learning/deep-learning models to generate recommendations through a simple web interface.

High-level workflow

User Input
    │
    ├── Soil & Environmental Parameters
    │        │
    │        └── Crop Recommendation Model
    │
    ├── Crop & Soil Information
    │        │
    │        └── Fertilizer Recommendation System
    │
    └── Plant Leaf Image
             │
             └── Deep Learning Disease Detection Model
                         │
                         └── Disease Information & Treatment

🚀 Features

🌱 Crop Recommendation

The crop recommendation module uses a trained machine-learning model to recommend a suitable crop based on soil and environmental conditions.

Inputs include:

Nitrogen

Phosphorus

Potassium

Temperature

Humidity

Soil pH

Rainfall

Output:

Recommended crop

🧪 Fertilizer Recommendation

The fertilizer recommendation module provides fertilizer guidance based on the selected crop and relevant soil conditions.

Output includes:

Recommended fertilizer

Additional guidance for improving crop conditions

🍃 Plant Disease Detection

Users can upload a plant-leaf image to identify potential diseases.

The disease-detection pipeline uses:

PyTorch

Torchvision

ResNet9-based architecture

A trained .pth model

Pillow for image processing

Output includes:

Predicted disease

Disease description

Recommended treatment/remedy

🌦️ Weather Integration

The application integrates weather information through an external weather API to support agricultural recommendations.

🖥️ Web Interface

The application is served through Flask and provides a browser-based interface for interacting with the ML/DL models.

🛠️ Technology Stack

Category

Technologies

Programming Language

Python

Web Framework

Flask

Frontend

HTML, CSS, JavaScript

Styling

Bootstrap / CSS

Machine Learning

Scikit-learn

Deep Learning

PyTorch, Torchvision

Data Processing

NumPy, Pandas

Image Processing

Pillow

HTTP / API Requests

Requests

Model Serialization

Pickle

Version Control

Git / GitHub

Deployment

Gunicorn

🧠 Machine Learning & Deep Learning

Crop Recommendation

The crop recommendation model is a trained Scikit-learn model stored in the models/ directory.

The model expects agricultural and environmental parameters such as N, P, K, temperature, humidity, pH, and rainfall.

Plant Disease Detection

The plant disease detection system uses a trained PyTorch model and the ResNet9 architecture defined in the project's utility modules.

The trained model is stored as:

models/plant_disease_model.pth

Model Compatibility

This repository contains previously trained model files. Some of these models were serialized with older versions of the ML libraries.

In particular, the crop recommendation model was created with:

scikit-learn 0.23.2

Therefore, the project intentionally uses an older dependency stack rather than automatically upgrading to the latest ML libraries.

Do not upgrade Scikit-learn, NumPy, or PyTorch without retraining/re-exporting the affected models.

📁 Project Structure

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
│   └── other application templates
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
├── Runtime.txt
├── .gitignore
└── README.md

The venv/ directory is a local Python virtual environment and should not be committed to GitHub.

⚙️ Installation & Setup

Prerequisites

For the current trained models, use:

Python 3.8.10

Newer Python versions may not work with the legacy PyTorch and Scikit-learn versions required by the existing models.

Verify Python

python --version

Expected:

Python 3.8.10

1. Clone the Repository

git clone https://github.com/bachusaketh/Smart-Farming.git
cd Smart-Farming

2. Create a Virtual Environment

Windows

py -3.8 -m venv venv

Activate it:

venv\Scripts\activate

You should see:

(venv) C:\...\Smart-Farming>

macOS / Linux

python3.8 -m venv venv
source venv/bin/activate

3. Verify the Environment

python --version

Expected:

Python 3.8.10

4. Install Dependencies

Install the regular dependencies:

python -m pip install --upgrade pip

python -m pip install -r requirements.txt

PyTorch 1.7.0

The project uses the legacy PyTorch 1.7.0 / Torchvision 0.8.0 stack.

If pip cannot locate the PyTorch packages from requirements.txt, install them using the PyTorch wheel repository:

python -m pip install torch==1.7.0+cu110 torchvision==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html

Then verify:

python -c "import torch; import torchvision; print('Torch:', torch.__version__); print('Torchvision:', torchvision.__version__)"

5. Configure the Weather API

The application uses a weather API through config.py.

Before publishing or sharing the project, make sure API credentials are not hard-coded or committed to GitHub.

A safer production setup is to store secrets in environment variables.

For example:

WEATHER_API_KEY=your_api_key_here

and load the value from the environment in config.py.

If your current config.py contains a real API key, rotate that key if it has already been pushed to a public repository.

6. Run the Application

With the virtual environment activated:

python app.py

The Flask development server should start at:

http://127.0.0.1:5000

Open that address in your browser.

🧪 Using the Application

Crop Recommendation

Open the Smart Farming application.

Navigate to the crop recommendation section.

Enter the required soil and environmental values.

Submit the form.

The trained ML model returns a recommended crop.

Fertilizer Recommendation

Select or provide the required crop/soil information.

Submit the form.

The fertilizer recommendation system returns the suggested fertilizer and guidance.

Plant Disease Detection

Open the disease detection section.

Upload a plant-leaf image.

Submit the image.

The deep-learning model predicts the disease.

The application displays disease information and recommended treatment.

📊 Data Sources

The project uses publicly available agricultural datasets and supporting data.

Crop Recommendation Dataset

Kaggle — Crop Recommendation Dataset:

https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset

Fertilizer Dataset

Harvestify fertilizer dataset:

https://github.com/Gladiator07/Harvestify/blob/master/Data-processed/fertilizer.csv

Plant Disease Dataset

Kaggle — New Plant Diseases Dataset:

https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset

Dataset licenses and usage terms should be reviewed before redistributing the original datasets.

📦 Important Model Files

The application depends on trained model artifacts stored in the repository.

models/
├── RandomForest.pkl
└── plant_disease_model.pth

These files are not ordinary source-code files. They are serialized model artifacts and may depend on specific versions of the libraries used when they were created.

If the models are retrained or replaced, update the dependency versions and documentation accordingly.

🔧 Troubleshooting

ImportError: cannot import name 'Markup' from 'flask'

The application imports Markup from markupsafe.

The correct import is:

from flask import Flask, render_template, request, redirect
from markupsafe import Markup

InconsistentVersionWarning from Scikit-learn

This usually means a serialized Scikit-learn model was created using a different Scikit-learn version.

For the current RandomForest.pkl, use:

scikit-learn==0.23.2

Do not upgrade Scikit-learn without validating the saved model.

node array from the pickle has an incompatible dtype

This indicates that the Scikit-learn version used to load the model is incompatible with the version used to create the model.

For this repository, use the pinned dependency versions in requirements.txt.

No matching distribution found for torch

The old PyTorch packages may require the PyTorch wheel repository.

Try:

python -m pip install torch==1.7.0+cu110 torchvision==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html

Port 5000 is already in use

Stop the existing Flask process or run the application on another port.

For example, if the application supports it:

app.run(port=5001)

Then open:

http://127.0.0.1:5001

🔒 Security Notes

Do not commit sensitive credentials such as:

Weather API keys

Passwords

Access tokens

Cloud credentials

Database credentials

Use environment variables or a local .env file for secrets.

Make sure .env is included in .gitignore.

🚀 Deployment

The project includes a Procfile and Gunicorn dependency for deployment environments that support WSGI applications.

For local development, use:

python app.py

For a production deployment, use a production WSGI server such as Gunicorn according to the requirements of the hosting platform.

The Flask development server should not be used as the production server.

🔮 Future Improvements

Potential improvements for future versions include:

Upgrade the ML/DL dependency stack after retraining the models.

Move API credentials completely to environment variables.

Add automated model evaluation and validation.

Add model performance metrics to the application.

Improve input validation and error handling.

Add responsive mobile-first UI improvements.

Add prediction history and analytics.

Add user authentication and personalized farm profiles.

Add additional crop and disease datasets.

Improve disease detection accuracy with model fine-tuning.

Add automated testing and CI/CD.

Containerize the application with Docker.

Deploy the application using a modern cloud platform.

🤝 Contributing

This project was developed as an academic/portfolio project.

Suggestions, bug reports, and improvements are welcome.

For significant changes:

Fork the repository.

Create a feature branch.

Make your changes.

Test the application locally.

Commit your changes with a clear message.

Open a pull request.

📜 License

This project is available under the license included in the repository.

See the LICENSE file for the complete license text.

👨‍💻 Author

Bachu Saketh

Computer Science Engineering — AI & ML

GitHub: https://github.com/bachusaketh

⭐ Acknowledgements

Scikit-learn for the machine-learning framework.

PyTorch and Torchvision for deep-learning functionality.

Flask for the web application framework.

Kaggle and the dataset contributors for agricultural datasets.

Open-source contributors whose libraries and resources support the project.

🌾 Project Summary

Smart Farming brings together machine learning, deep learning, agricultural data, and a web interface to provide practical recommendations for crop selection, fertilizer usage, and plant disease identification.

The project demonstrates an end-to-end workflow:

Agricultural Data
       ↓
Data Processing
       ↓
ML / DL Models
       ↓
Model Inference
       ↓
Flask Web Application
       ↓
Agricultural Recommendation
