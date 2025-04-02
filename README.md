<!-- Back to top compatibility -->
<a name="readme-top"></a>

<!-- PROJECT BANNER -->
![project_banner](https://your-image-link-here) <!-- Optional if you have a banner -->

<h1 align="center">Flooded Area Classification using Sentinel-2 and NDWI</h1>
<p align="center">
  Using Random Forest classification and Sentinel-2 imagery to detect flood-affected land.
</p>
<br />

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About the Project</a>
      <ul>
        <li><a href="#background">Background</a></li>
        <li><a href="#the-sentinel-2-satellite">The SENTINEL-2 Satellite</a></li>
        <li><a href="#remote-sensing-method---ndwi">Remote Sensing Method – NDWI</a></li>
        <li><a href="#machine-learning-method---random-forest">Machine Learning Method – Random Forest</a></li>
      </ul>
    </li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#datasets-used">Datasets Used</a></li>
      </ul>
    </li>
    <li><a href="#environmental-cost">Environmental Cost</a></li>
    <li><a href="#video-overview">Video Overview</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#references">References</a></li>
  </ol>
</details>

---

<!-- ABOUT THE PROJECT -->
# About the Project

This project is part of the GEOL0069 AI4EO course at University College London. The goal is to detect flood-affected areas using Sentinel-2 optical satellite imagery by applying a widely used remote sensing index (NDWI) and a supervised machine learning algorithm (Random Forest). The project outputs include a binary classification map (flooded / non-flooded) and an analysis of computational/environmental impact.

---

## Background

Floods are one of the most destructive natural disasters globally, affecting millions of people every year. Early and accurate detection of flood extent using satellite imagery is a vital tool for disaster response, infrastructure planning, and humanitarian relief.

Compared to manual surveying, remote sensing allows for rapid, scalable, and low-cost flood detection. By combining multispectral satellite data with machine learning, this project demonstrates how flooded areas can be automatically identified with minimal manual input.

---

## The SENTINEL-2 Satellite

SENTINEL-2 is a European Earth observation mission with two satellites (S2A & S2B), designed to provide high-resolution optical imagery for land monitoring. Each carries the Multi-Spectral Instrument (MSI), capturing 13 spectral bands:

- 4 bands at 10m (visible and NIR)
- 6 bands at 20m (including SWIR)
- 3 bands at 60m (atmospheric correction)

These bands make Sentinel-2 suitable for applications such as vegetation monitoring, water detection, and land use classification.

---

## Remote Sensing Method – NDWI

To extract water bodies, the Normalized Difference Water Index (NDWI) is used:


- Green = Band 3 (560 nm)
- NIR = Band 8 (842 nm)

NDWI emphasizes water features while suppressing soil and vegetation. Pixels with higher NDWI values typically represent water surfaces, especially useful for flood detection after major rainfall events.

---

## Machine Learning Method – Random Forest

To automate classification, we use a **Random Forest** classifier. It is chosen for its:
- Simplicity
- Fast training
- High accuracy on small datasets

### Workflow:
1. Calculate NDWI from Sentinel-2 imagery
2. Create labeled training samples (flooded/non-flooded)
3. Train Random Forest on NDWI data
4. Apply model to full scene
5. Generate binary flood classification map

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

# Getting Started

### Requirements:
- Python 3.x
- `rasterio`, `numpy`, `scikit-learn`, `matplotlib`, `pandas`
- Jupyter or Google Colab

### Instructions:
1. Clone this repo and open the `flood_classification.ipynb` notebook
2. Modify file paths if needed
3. Run all cells in order
4. Visual outputs will include NDWI images and classification maps

---

## Datasets Used

Sentinel-2 L2A imagery was used (surface reflectance). Pre- and post-flood scenes were selected from a recent flood-prone region (e.g. Italy, Bangladesh, UK).

Images were downloaded from the [Copernicus Dataspace Browser](https://dataspace.copernicus.eu/).

---

# Environmental Cost

The model was trained on a CPU with no GPU acceleration.

| Component        | Details                          |
|------------------|----------------------------------|
| Model            | Random Forest (100 trees)        |
| Training time    | ~15 seconds                      |
| Platform         | Local CPU (Intel i5)             |
| CO₂ estimate     | ~0.005 kg                        |

Tools like [CodeCarbon](https://mlco2.github.io/codecarbon/) can be used for more detailed reporting.

---

# Video Overview

A short walkthrough video is included, covering:
- Code logic
- NDWI map creation
- Classification results
- Environmental discussion

[🔗 Link to video once uploaded]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

# License

Distributed under the MIT License. See `LICENSE.txt` for more information.

---

# Contact

[Your Name]  
[Your Email]  
University College London  
GEOL0069 AI4EO

---

# References

- McFeeters, S.K. (1996). NDWI for water body mapping.
- Xu, H. (2006). Modified NDWI.
- Breiman, L. (2001). Random Forests.
- Sentinel-2 ESA Documentation: https://sentinel.esa.int/web/sentinel/missions/sentinel-2

<p align="right">(<a href="#readme-top">back to top</a>)</p>
