# Image Classifier

An AI-powered web application that identifies what's in any photograph. Upload an image and the app returns a ranked list of predictions with confidence scores, powered by a deep learning model running locally in your browser.

Built as part of the **AI Center of Excellence (Accelerated by NVIDIA)** internship.

---

## What it does

You upload a photo, and the app tells you what's most likely in it — along with how confident it is. Instead of a single answer, it shows the top five predictions, each with a confidence percentage and a visual probability bar.

- Recognises **1,000 everyday object categories** (animals, objects, food, vehicles, and more)
- Shows a **ranked probability distribution**, not just one label
- Processes images **entirely in memory** — nothing is ever saved to disk
- Runs **locally** on ordinary hardware, no GPU required

---

## How it works

The app uses **transfer learning** with **MobileNetV2**, a convolutional neural network pre-trained by Google on the ImageNet dataset of over a million images. Rather than training a model from scratch, it reuses this proven model and wraps it in a clean web interface.

When you classify an image, three things happen:

1. **Preprocessing** — the image is resized and center-cropped to 224×224 pixels, the size the model expects.
2. **Inference** — the neural network analyses the pixels and produces a probability for each of its 1,000 categories.
3. **Readout** — the top five predictions are displayed, ranked from most to least likely.

---

## Tech stack

| Technology | Purpose |
|------------|---------|
| Python | Core language for the backend and AI integration |
| Flask | Web framework that serves the app and handles requests |
| TensorFlow / Keras | Loads the model and runs the image classification |
| MobileNetV2 | Pre-trained CNN that recognises 1,000 categories |
| Pillow | Resizes and preprocesses uploaded images |
| NumPy | Numerical operations to prepare image data |
| HTML / CSS / JavaScript | Front-end interface with upload and live readout |
| Waitress | Production server option for deployment |

---

## Project structure

```
files/
├── app.py                  # Flask entry point — routes, API, error handling
├── config.py               # App configuration
├── requirements.txt        # Python dependencies
├── ml/
│   ├── __init__.py
│   ├── model.py            # Loads MobileNetV2, keeps it in memory
│   ├── predict.py          # Runs inference, formats predictions
│   └── preprocess.py       # Resizes and prepares images
├── utils/
│   ├── __init__.py
│   └── validators.py       # Validates uploaded files
├── templates/
│   ├── base.html
│   ├── index.html          # Main page
│   ├── 404.html
│   └── 500.html
├── static/
│   ├── css/
│   │   └── style.css       # Styling
│   └── js/
│       └── main.js         # Front-end logic
└── venv/                   # Virtual environment (not committed)
```

---

## Setup

### Prerequisites

- **Python 3.12** (TensorFlow does not yet support 3.13 or 3.14)

Check your version:

```powershell
py -0p
```

If you don't have 3.12, install it from [python.org](https://www.python.org/downloads/) and tick **"Add python.exe to PATH"** during installation.

### Installation

**1. Open a terminal in the project folder** and create a virtual environment:

```powershell
py -3.12 -m venv venv
```

**2. Activate it:**

```powershell
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks the script, run this once, then activate again:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**3. Install dependencies:**

```powershell
pip install -r requirements.txt
```

This downloads TensorFlow and the other packages (a few hundred MB — give it a minute).

---

## Running the app

With the virtual environment active:

```powershell
python app.py
```

You'll see:

```
* Running on http://127.0.0.1:5000
```

Open **http://127.0.0.1:5000** in your browser.

To stop the server, click the terminal and press **Ctrl + C**.

---

## Usage

1. Open the app in your browser.
2. Click **"Choose an image"** or drag a photo into the drop zone.
3. Click **"Classify image"**.
4. View the ranked predictions with confidence scores.

**Tip:** the first classification takes a few seconds while the model loads into memory. Every prediction after that is fast.

Supported formats: JPG, PNG, WebP, BMP, GIF, up to 8 MB.

---

## Privacy

Every uploaded image is processed in memory and discarded the moment the prediction is returned. No image is written to disk, logged, or sent anywhere. The entire app — model, server, and processing — runs on your own machine.

---

## Limitations

- Recognises only the 1,000 categories the model was trained on; unfamiliar subjects are matched to the closest known category.
- Accuracy can drop on unusual, low-quality, or heavily cropped images.
- Handles one image at a time (no batch or video processing).

---

## Future scope

- Fine-tuning on a custom dataset for a specific domain
- Batch and video input support
- A choice of different models
- Richer analysis and visualisation of results

---

## Author

**Srishti** — 20241CSE0634
B.Tech, Computer Science and Engineering
Presidency University, Bengaluru

Developed under the guidance of Bhuvaneshwari Patil and Gyanesh Varma.# Image-classifier-
