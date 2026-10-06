# 🐾 Animal Vision AI --- Animal Image Classifier

A deep-learning based animal image classification project built with
**PyTorch**, **Torchvision**, and **ResNet50**. The model classifies
uploaded animal images into one of **151 classes** and provides the
predicted class and confidence score through a **Streamlit web
interface**.

## ✨ Project Highlights

-   🧠 Pretrained **ResNet50** transfer-learning model
-   🐾 **151 animal classes**
-   🖼️ Image upload and prediction through Streamlit
-   📊 Top-5 prediction probabilities
-   🎯 Confidence score for the predicted class
-   ⚡ GPU training with NVIDIA Tesla T4 in Google Colab
-   🔥 Mixed-precision training with PyTorch AMP
-   📈 Training/validation accuracy and loss visualization
-   🧪 Separate validation and test sets
-   💾 Best model checkpoint saved as `best_animal_classifier.pth`

## 📊 Dataset

The project uses the `animal-image-classification` dataset repository
and its `dataset/animals` directory.

The notebook reports:

  Property                        Value
  ------------------- -----------------
  Total images                    6,270
  Animal classes                    151
  Training images                 5,016
  Validation images                 627
  Test images                       627
  Split                 80% / 10% / 10%

The dataset contains class folders using scientific-species-style names
such as:

-   `panthera-tigris`
-   `panthera-leo`
-   `panthera-onca`
-   `ursus-arctos-horribilis`
-   `ailuropoda-melanoleuca`
-   `giraffa-camelopardalis`

## 🧠 Model Architecture

The project uses **ResNet50 with pretrained ImageNet weights**.

The original training pipeline:

``` text
Input Image
     ↓
Resize / Data Augmentation
     ↓
224 × 224 Image
     ↓
ImageNet Normalization
     ↓
Pretrained ResNet50
     ↓
Dropout (0.4)
     ↓
Fully Connected Layer
     ↓
151 Animal Classes
     ↓
Softmax Probabilities
```

The original notebook freezes the pretrained ResNet50 layers and trains
the final classification layer.

## 🖼️ Image Preprocessing

### Training

The training pipeline applies:

-   Resize to 256 × 256
-   Random resized crop to 224 × 224
-   Random horizontal flip
-   Random rotation up to 10°
-   Color jitter
-   Tensor conversion
-   ImageNet normalization

### Validation / Test

Validation and test images are:

-   Resized to 224 × 224
-   Converted to tensors
-   Normalized using ImageNet mean and standard deviation

## ⚙️ Training Configuration

  Setting           Value
  ----------------- ------------------
  Model             ResNet50
  Classes           151
  Batch size        64
  Epochs            5
  Optimizer         AdamW
  Learning rate     0.001
  Weight decay      0.0001
  Loss              CrossEntropyLoss
  Dropout           0.4
  GPU               NVIDIA Tesla T4
  Mixed precision   Enabled

## 📈 Training Results

The original notebook achieved:

-   **Best validation accuracy: 85.49%**
-   **Test accuracy: 84.85%**

Training history:

    Epoch   Train Accuracy   Validation Accuracy
  ------- ---------------- ---------------------
        1           22.73%                62.04%
        2           59.57%                78.95%
        3           70.65%                82.30%
        4           74.16%                85.01%
        5           76.77%                85.49%

> **Note:** Model test/validation accuracy and the confidence shown for
> a single uploaded image are different measurements. A correct model
> can still produce a relatively low confidence score for an individual
> image.

## 🌐 Streamlit Frontend

The project includes a Streamlit frontend called **Animal Vision AI**.

### Frontend features

-   📤 Upload an animal image
-   🖼️ Preview the uploaded image
-   🎯 Display predicted animal
-   📊 Display confidence percentage
-   🏆 Show top-5 predictions
-   🧠 Display model information
-   💻 CPU/GPU inference support
-   ⚠️ Confidence-level feedback

Example workflow:

``` text
Upload Image
     ↓
Image Preprocessing
     ↓
ResNet50 Inference
     ↓
Softmax
     ↓
Top Prediction + Confidence
     ↓
Top-5 Predictions
```

## 📁 Project Structure

``` text
animal-classifier/
│
├── app.py
├── best_animal_classifier.pth
├── requirements.txt
├── README.md
│
└── AI_Image_classifier.ipynb
```

### Important files

  File                           Purpose
  ------------------------------ -----------------------------
  `app.py`                       Streamlit web application
  `best_animal_classifier.pth`   Trained ResNet50 checkpoint
  `requirements.txt`             Python dependencies
  `AI_Image_classifier.ipynb`    Complete training notebook
  `README.md`                    Project documentation

## 🚀 Run the Project Locally

### 1. Clone the GitHub repository

``` bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd animal-classifier
```

### 2. Create a virtual environment

Windows:

``` powershell
py -3.14 -m venv .venv
```

Activate it:

``` powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

``` powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Add the trained model

Place:

``` text
best_animal_classifier.pth
```

in the same directory as:

``` text
app.py
```

Your folder should look like:

``` text
animal-classifier/
├── app.py
├── best_animal_classifier.pth
├── requirements.txt
└── README.md
```

### 5. Start Streamlit

``` powershell
streamlit run app.py
```

Open the local Streamlit address shown in the terminal, normally:

``` text
http://localhost:8501
```

## ☁️ Training in Google Colab

The training notebook is designed to use a **Tesla T4 GPU**.

The notebook checks CUDA availability before training:

``` python
torch.cuda.is_available()
```

The trained checkpoint is saved as:

``` text
/content/best_animal_classifier.pth
```

To download it from Colab:

``` python
from google.colab import files

files.download("/content/best_animal_classifier.pth")
```

## 🔬 Training Workflow

``` text
Dataset
   ↓
Dataset Inspection
   ↓
ImageFolder
   ↓
80 / 10 / 10 Split
   ↓
Data Augmentation
   ↓
ResNet50 Pretrained Model
   ↓
Replace Classification Head
   ↓
AdamW Optimizer
   ↓
Mixed Precision Training
   ↓
Validation
   ↓
Save Best Checkpoint
   ↓
Test Evaluation
   ↓
Streamlit Deployment
```

## 🧪 Evaluation

The test set contains **627 images**.

The notebook evaluates the trained model using top-1 classification
accuracy:

``` text
Test Accuracy: 84.85%
```

## 🛠️ Technologies Used

-   Python
-   PyTorch
-   Torchvision
-   ResNet50
-   PIL / Pillow
-   Matplotlib
-   Streamlit
-   Google Colab
-   CUDA
-   NVIDIA Tesla T4

## 🔮 Future Improvements

Possible improvements for future versions:

-   Fine-tune additional ResNet50 layers
-   Train for more epochs
-   Add learning-rate scheduling
-   Add early stopping
-   Add confusion matrix
-   Add precision, recall, and F1-score
-   Improve class balancing
-   Add Grad-CAM visual explanations
-   Add prediction history
-   Add drag-and-drop image upload
-   Deploy the Streamlit application online
-   Add a REST API for model inference

## ⚠️ Limitations

The model is trained on a fixed set of 151 classes. Images belonging to
classes outside this set may be incorrectly classified into one of the
known classes.

The confidence score should therefore be interpreted as the model's
probability distribution across its known classes, not as a guaranteed
measure of real-world correctness.

## 👨‍💻 Author

**Rohit Maurya**

Computer Science & Engineering Student

## ⭐ Project Goal

The goal of this project is to demonstrate a complete deep-learning
workflow:

**Dataset → Preprocessing → Transfer Learning → Training → Evaluation →
Model Export → Streamlit Deployment**

If you find the project useful, consider giving the repository a ⭐ on
GitHub.
