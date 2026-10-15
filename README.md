# G.O.A.T Vision — Soccer Play Classifier

G.O.A.T Vision (Game Outcome Action Tracker) is a computer vision application that classifies soccer images into five play categories using ResNet50 transfer learning and a Streamlit interface.

**Developed by:** [Samira Gevara](https://github.com/samirag2010)  
**Status:** Working prototype

[Live Demo](https://goatvision-soccer.streamlit.app/) | [Demo Video](https://youtu.be/KCoNR_yaisQ) | [Project Presentation](docs/presentation.pdf)

## Project Overview

This project explores how computer vision can distinguish soccer plays from still images. Users upload an image and receive a predicted category with a breakdown of the model’s class probabilities.

The project demonstrates dataset preparation, transfer learning, model evaluation, and application development.

## Features

- Upload JPG, JPEG, or PNG images.
- Classify images into five categories:
  - Corner Kick
  - Free Kick
  - Penalty Kick
  - Shot
  - Yellow Card
- Display the predicted category and class probabilities.
- Upload MP4 or MOV files through an experimental video feature.

**Video limitation:** The current implementation extracts and classifies the first readable frame. It does not analyze an entire video or track plays over time.

## Screenshots

### Application Interface
![GOATVision interface](results/DEMO_GV_Interface.png)

### Example Prediction
![GOATVision prediction](results/DEMO_GV_Prediction.png)

## My Contributions

- Curated and cleaned a custom dataset of soccer images.
- Developed and experimented with a PyTorch transfer-learning workflow using ResNet50.
- Applied image preprocessing and training augmentation.
- Evaluated validation performance and examined confusion between similar play categories.
- Built the Streamlit interface and connected it to the saved model.
- Documented project findings, demonstrations, and limitations.

AI tools supported project planning, debugging, implementation guidance, and documentation. Dataset preparation, code execution, and model experimentation were performed by Samira Gevara.

See the [AI Usage Log](docs/AI_usage_log.md) for additional details.

## Technologies

| Area | Tools |
|---|---|
| Programming | Python |
| Model development | PyTorch, torchvision, ResNet50 |
| Evaluation | scikit-learn, matplotlib |
| Interface | Streamlit |
| Development environment | Google Colab |
| Model download | Google Drive and gdown |
| Video frame extraction | OpenCV |
| Version control | Git and GitHub |

## How It Works

1. The user uploads a soccer image.
2. The application converts the image to RGB.
3. The image is resized to 224 × 224 pixels and normalized.
4. The saved ResNet50 classifier processes the image.
5. The application displays the predicted class and probability breakdown.

The training workflow uses transfer learning from ImageNet-pretrained ResNet50 features. At application startup, the app constructs the model architecture and loads the saved project weights.

Training augmentation includes horizontal flips and color jitter. These random transformations are not applied to uploaded images during inference.

## Dataset

The project documentation records **146 curated images** across five categories:

| Dataset Label | Category |
|---|---|
| corner_kick | Corner Kick |
| free_kick | Free Kick |
| penalty_kick | Penalty Kick |
| shot | Shot |
| yellow_card | Yellow Card |

Images were manually reviewed to remove irrelevant or ambiguous examples.

See the [dataset notes](data/README.md) and [project notebooks](notebooks/) for available supporting material.

## Evaluation

**Reported validation accuracy: 82.14%.**

This result reflects the project’s small validation dataset. It should not be interpreted as expected accuracy across all soccer images or real-world matches.

Evaluation identified confusion between visually similar categories, including shots, penalty kicks, and corner kicks.

The displayed prediction probabilities reflect the model’s relative preference among its five categories. They are not a calibrated guarantee that a prediction is correct.

## Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/samirag2010/GOATVision.git
cd GOATVision
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it using the command for your system:

**Windows PowerShell**
```powershell
.venv\Scripts\Activate.ps1
```

**macOS / Linux**
```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Start the application

```bash
python -m streamlit run app.py
```

### Model Download

On first launch, the application downloads `goatvision_model_state_dict.pth` from its configured Google Drive location if the file is missing.

Internet access and access to the hosted model are required. Later launches reuse the local file.

The application supports CPU execution and selects CUDA when available.

Dependencies are not fully pinned, so compatibility may vary across environments.

## Repository Guide

| Path | Purpose |
|---|---|
| [app.py](app.py) | Streamlit interface and model inference |
| [requirements.txt](requirements.txt) | Python dependencies |
| [notebooks/](notebooks/) | Exploration and model development |
| [data/README.md](data/README.md) | Dataset notes |
| [results/](results/) | Demonstration screenshots |
| [docs/presentation.pdf](docs/presentation.pdf) | Project presentation |
| [docs/AI_usage_log.md](docs/AI_usage_log.md) | AI assistance documentation |
| [LICENSE](LICENSE) | Repository license |

## Limitations

- The small dataset limits generalization.
- A still image may not contain enough context to distinguish similar plays.
- The classifier selects among five known categories and does not reliably reject unrelated images.
- Experimental video support classifies one frame rather than a complete sequence.
- Model availability depends on external hosting.
- The application is a prototype, not a production match-analysis system

## Future Improvements

- Expand the dataset with more diverse labeled images.
- Document reproducible training settings and dataset splits.
- Evaluate performance on a separate test set.
- Add per-class evaluation results and investigate unrelated-image handling.
- Improve model-download error handling and video resource cleanup.
- Explore video sequences and object detection.



