# Predicting Focal Colours From Natural Images

A computational analysis that predicts focal colour categories from natural images using K-means clustering, validated against the World Color Survey (WCS) data.

## Overview

This project investigates whether focal colour categories can be predicted from the colour distribution of natural images. By extracting and clustering colour data from thousands of natural images, we test if the resulting clusters match the focal colours identified across different languages in the World Color Survey.

The analysis shows that colour clusters derived from natural images align significantly with cross-linguistic focal colours, with an average improvement of **39.7%** over random baselines.

## Features

- Extract colour samples from large image datasets (Tiny ImageNet)
- Filter colours based on lightness and chroma criteria
- Perform K-means clustering in LAB colour space
- Compare predictions against WCS focal colour data
- Statistical analysis with t-tests and effect sizes
- Generate visualizations of predicted focal colours and performance metrics

## Project Structure

```
focal-colour-predictor/
├── project.ipynb              # Main analysis notebook\
├── projectpreliminary.ipynb              # Main analysis notebook
├── wcs_helper_functions.py    # Helper functions (ommitted)
├── WCS_data_core/            # World Color Survey data files (ommitted)
│   ├── term.txt              # Colour naming data
│   ├── foci-exp.txt          # Focal colour data
│   ├── chip.txt              # Colour chip specifications
│   ├── spkr-lsas.txt         # Speaker demographic data
│   └── cnum-vhcm-lab-new.txt # LAB colour values for chips
├── requirements.txt          # Python dependencies
└── README.md                # This file
```

## Installation

### Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab

### Setup

1. Clone or download this repository

2. Create a virtual environment (recommended):
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

3. Install required dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Running the Analysis

1. Open the Jupyter notebook:
```bash
jupyter notebook project.ipynb
```

2. The notebook will automatically:
   - Download the Tiny ImageNet dataset via kagglehub
   - Load WCS data from [WCS_data_core/](WCS_data_core/)
   - Extract colour samples from images
   - Perform K-means clustering for N=2 to N=11 terms
   - Evaluate predictions against WCS focal colours
   - Generate visualizations and save results

### Key Parameters

You can modify these constants in the notebook:

- `MAX_IMAGES`: Number of images to process (default: 10000)
- `PIXELS_PER_IMAGE`: Colour samples per image (default: 100)
- `IMAGE_PATH`: Path to image dataset

## Methodology

### Data Processing

1. **Image Sampling**: Extracts pixel colours from 10,000 natural images
2. **Colour Filtering**: Filters pixels based on:
   - Lightness (L < 25 or L > 80)
   - Chroma (saturation > 30)
3. **Colour Space**: Converts RGB to LAB colour space for perceptual uniformity

### Clustering

- **Algorithm**: K-means clustering (k=2 to 11)
- **Colour Space**: CIELAB (perceptually uniform)
- **Evaluation Metrics**:
  - Silhouette score (cluster separation)
  - Inertia (within-cluster variance)
  - ΔE distance to WCS focal colours

### Validation

Predictions are compared against WCS focal colours using:
- Mean Euclidean distance in LAB space (ΔE)
- Paired t-tests against random baselines
- Cohen's d effect sizes

## Results

### Key Findings

- **Average improvement over random**: 39.7%
- **Best performance**: N=4 terms (69.3% improvement)
- **Statistical significance**: 6/7 cases with p < 0.05
- **Mean effect size**: Cohen's d = 15.98 (very large)

### Generated Outputs

The notebook produces:

1. **predicted_focal_colours.png** - Visualization of predicted focal colours for N=2 to 11
2. **model_comparison.png** - K-means vs. random baseline comparison
3. **statistical_analysis.png** - Improvement percentages and effect sizes
4. **colour_evolution_hierarchy.png** - Colour term evolution hierarchy
5. **silhouette_inertia_plots.png** - Clustering performance metrics
6. **results_kmeans.csv** - Numerical results for K-means predictions
7. **results_statistics.csv** - Statistical test results

## Dependencies

- numpy - Numerical computing
- pandas - Data manipulation
- matplotlib - Visualization
- scikit-learn - Machine learning (K-means)
- scipy - Statistical analysis
- seaborn - Enhanced visualizations
- torch - PyTorch (if needed for extensions)
- scikit-image - Image processing and colour space conversion
- kagglehub - Dataset download
- tqdm - Progress bars

## Data Sources

### World Color Survey (WCS)
- **Source**: http://www1.icsi.berkeley.edu/wcs/data.html
- **Description**: Cross-linguistic colour naming data from 110 languages
- **Credit**: Original demo code by Vasilis Oikonomou, Joshua Abbott, Jessie Salas, Janaki Vivrekar, Samantha Quinto, and Elva Xinyi Chen

### Image Dataset
- **Source**: Tiny ImageNet dataset via Kaggle
- **Size**: 10,000 test images
- **Purpose**: Natural image colour distribution sampling

## Credits

**Original WCS Demo Code**:
- Vasilis Oikonomou
- Joshua Abbott
- Jessie Salas
- Janaki Vivrekar
- Samantha Quinto
- Elva Xinyi Chen

**Copyright**: Yang Xu @ 2019, University of Toronto
**Correspondence**: yang_xu_ch -AT- cs dot toronto dot edu

**Course**: COG 260 - Data, Computation and The Mind

[Code](https://www.cs.toronto.edu/~yangxu/wcs_data_notebook.zip)

## License

Please refer to the original WCS data license and citation requirements at the [WCS website](http://www1.icsi.berkeley.edu/wcs/data.html).

## Troubleshooting

### Common Issues

1. **Dataset download fails**: Ensure you have a stable internet connection and sufficient disk space (~500MB)
2. **Memory errors**: Reduce `MAX_IMAGES` or `PIXELS_PER_IMAGE` parameters
3. **Slow processing**: Consider using a subset of images for initial testing

### Performance Tips

- Use GPU acceleration for larger datasets (requires PyTorch with CUDA)
- Reduce `n_init` parameter in K-means for faster convergence
- Sample fewer pixels per image for quicker prototyping

## Further Reading

- Berlin, B., & Kay, P. (1969). *Basic Color Terms: Their Universality and Evolution*
- Kay, P., & Regier, T. (2003). Resolving the question of color naming universals
- World Color Survey: http://www1.icsi.berkeley.edu/wcs/
