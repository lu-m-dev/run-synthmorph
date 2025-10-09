# SynthMorph Registration and Analysis Pipeline

A Python pipeline for automated image registration using [SynthMorph](https://martinos.org/malte/synthmorph/) and subsequent tumor location analysis. The tool recursively processes directories containing neuroimaging data, generates registration scripts, and analyzes transformed tumor segmentations to determine anatomical locations.

## Overview

This pipeline includes:
- **Script Generation**: Recursively scans directories for NIfTI images and generates SynthMorph registration shell scripts
- **Registration Processing**: Registers moving images to atlas and applies transformations to tumor segmentations  
- **Location Analysis**: Analyzes transformed tumor segmentations to determine percentage overlap with brain regions

## Workflow

1. **Configure paths and registration parameters** in `config/config.yaml` and `config/register.yaml`
2. **Generate SynthMorph registration script** using `generate_script.ipynb`
3. **Execute script** on Unix system with SynthMorph installed
4. **Analyze results** using `analyze_output.ipynb`
5. **[OPTIONAL] Visualize image overlay** in `visualize_overlay.ipynb`

## Files

### Notebooks
- `generate_script.ipynb`: Generates SynthMorph registration shell script.
- `analyze_output.ipynb`: Analyzes transformed segmentations for tumor location percentages. Percentages calculated as `[voxels overlapped with each label] / [total tumor voxels]`. The percentages do not sum up to 100%.
- `visualize_overlay.ipynb`: Visualizes parcellation overlaid on atlas, transformed images overlaid on atlas, transformed tumor segmentaion overlaid on atlas.

### Configuration Files
- `config.yaml`: Input/output paths and processing parameters
- `register.yaml`: SynthMorph registration settings (model, lambda, steps, extent)
- `apply.yaml`: Transformation settings (interpolation method, data type, fill value)

### Data Requirements
- Atlas with corresponding parcellation and label files

## Output
- `generate_script.ipynb` generates `output/run_synthmorph.sh`
- `analyze_output` generates `output/locations.csv`

## Installation

```bash
pip install -e .
```

Or with uv:
```bash
uv sync
```
