# age-classifier

A FastAI-based image classification project that categorizes face images into three age groups: **young**, **middle-aged**, and **old**.

## 📦 Repository Structure

```
├── data/                       # (Optional) Raw dataset or link instructions
├── notebooks/                  # Jupyter/Colab notebooks
│   └── finetune_age_classifier.ipynb  # Step-by-step finetuning and evaluation
├── models/                     # Exported model files
│   └── best_model.pkl      # Trained FastAI learner
├── app/                        # Gradio application for inference
│   ├── app.py                  # Gradio interface code
│   └── requirements.txt        # Python dependencies for the app
├── README.md                   # This file
└── LICENSE                     # Project license
```

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<Balghi>/age-classifier.git
cd age-classifier
```

### 2. Prepare the dataset

Download the **Faces Age Detection** dataset from Kaggle:

```bash
kaggle datasets download arashnic/faces-age-detection-dataset -q
unzip faces-age-detection-dataset.zip -d data/
```

Ensure you have a `data/` folder containing:

* `images/` directory with face images
* `train.csv` listing image filenames and labels (`young`, `middle`, `old`)

### 3. Finetune the model

Open the Colab/Jupyter notebook and follow the sections in order:

1. **DataBlock construction**: defining `ImageBlock` and `CategoryBlock` with transforms.
2. **Baseline training**: fine-tune ResNet34 for initial accuracy.
3. **Learning rate finder**: select optimal learning rate.
4. **Transfer learning**: freezing/unfreezing and discriminative learning rates.
5. **Deciding epochs**: guidelines on epoch counts and early stopping.
6. **Model capacity**: changing backbones or batch sizes.

```bash
# Example: run notebook
jupyter notebook notebooks/finetune_age_classifier.ipynb
```

After training, your model will be exported to `models/best_model.pkl`.

### 4. Run the Gradio App

Install dependencies and launch inference:

```bash
cd app
pip install -r requirements.txt
python app.py
```

Then open `http://localhost:7860` in your browser to upload face images and see age predictions.

### 5. Deploy to Hugging Face Spaces

1. Create a new Space (Gradio SDK) on Hugging Face.
2. Push the `app/` folder (including `app.py`, `requirements.txt`, and `age_classifier.pkl`).
3. Ensure your `README.md` has the proper front-matter for the Space:

```yaml
---
title: Age Category Classifier
emoji: "🧓"
colorFrom: "blue"
colorTo: "purple"
sdk: gradio
sdk_version: "3.20.0"
app_file: app.py
pinned: false
---
```

Visit the Space URL to test your deployed app.

## 📝 License

This project is released under the MIT License. See [LICENSE](LICENSE) for details.

---

*Happy modeling!*
