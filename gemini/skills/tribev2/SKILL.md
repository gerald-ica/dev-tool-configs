---
name: tribev2
description: Meta's TRIBE v2 foundation model for predicting fMRI brain responses to video, audio, and text stimuli. Use when working with brain encoding models, fMRI prediction, multimodal neuroscience, brain-AI alignment, cortical surface mapping, or in-silico neuroscience research.
version: "1.0.0"
license: CC-BY-NC-4.0
metadata:
  homepage: "https://github.com/facebookresearch/tribev2"
  openclaw:
    emoji: "🧠"
    homepage: "https://github.com/facebookresearch/tribev2"
    requires:
      bins:
        - python3
        - pip3
---

# TRIBE v2

**A Foundation Model of Vision, Audition, and Language for In-Silico Neuroscience** by Meta/Facebook Research.

Predicts fMRI brain responses to naturalistic stimuli (video, audio, text) by combining state-of-the-art pretrained models into a unified Transformer architecture that maps multimodal representations onto the cortical surface.

## What It Does

- Predicts fMRI activity across ~20,000 cortical vertices on the fsaverage5 mesh
- Accepts video, audio, or text input with automatic preprocessing
- Provides population-average brain response predictions
- Accounts for hemodynamic lag (5-second offset)
- Supports subject-specific modeling with personalized embeddings

## Setup

```bash
# Clone
git clone https://github.com/facebookresearch/tribev2.git
cd tribev2

# Basic install (inference only)
pip install -e .

# With brain visualization (PyVista + Nilearn)
pip install -e ".[plotting]"

# With training dependencies (PyTorch Lightning)
pip install -e ".[training]"
```

**Requirements:** Python >=3.11, PyTorch >=2.5.1,<2.7

## Usage

### Basic Inference - Predict Brain Response from Video
```python
from tribev2 import TribeModel

model = TribeModel.from_pretrained("facebook/tribev2", cache_folder="./cache")

# From video (extracts audio, transcribes, processes all modalities)
df = model.get_events_dataframe(video_path="path/to/video.mp4")
preds, segments = model.predict(events=df)
print(preds.shape)  # (n_timesteps, n_vertices)
```

### From Audio Only
```python
df = model.get_events_dataframe(audio_path="path/to/audio.wav")
preds, segments = model.predict(events=df)
```

### From Text (auto-converts to speech, then transcribes)
```python
df = model.get_events_dataframe(text_path="path/to/text.txt")
preds, segments = model.predict(events=df)
```

### Training

```bash
# Local test run
python -m tribev2.grids.test_run

# Production on Slurm
DATAPATH=/path/to/data SAVEPATH=/path/to/save python -m tribev2.grids.run_cortical

# Subcortical variant
python -m tribev2.grids.run_subcortical
```

## Architecture

- **Feature Extractors**: Integrates multiple SOTA models for video encoding, audio representation, and text embeddings
- **Transformer Backbone**: Unified architecture that fuses multimodal features
- **Cortical Mapper**: Projects fused representations onto brain surface vertices
- **Layer Aggregation**: Flexible aggregation across network layers and modalities
- **Temporal Smoothing**: Gaussian kernel-based smoothing for stable predictions
- **Subject Embeddings**: Optional per-subject layers for personalized predictions

## Key Capabilities

| Feature | Description |
|---------|-------------|
| Multimodal input | Video, audio, text - with automatic preprocessing pipeline |
| Brain prediction | ~20,000 cortical vertices on fsaverage5 mesh |
| Hemodynamic lag | Automatic 5-second offset compensation |
| Multi-study support | Load and process data from multiple fMRI studies |
| Visualization | Cortical surface plots via PyVista and Nilearn |
| Population model | Average-subject predictions generalizable across subjects |
| HuggingFace | Pretrained weights at `facebook/tribev2` |

## Use Cases

- Predicting brain activity from naturalistic video/audio/text stimuli
- Brain-AI alignment research (mapping AI representations to neural activity)
- Understanding how brains process multimodal information
- Computational neuroscience experiments without biological data collection
- Comparing AI model representations to cortical patterns
- Building on TRIBE v2 for downstream neuroscience applications

## When to Use This Skill

- Working with fMRI data or brain encoding models
- Building multimodal neuroscience pipelines
- Predicting brain responses to media content
- Researching brain-AI alignment or neural representation
- Running in-silico neuroscience experiments
- Visualizing cortical surface activations
