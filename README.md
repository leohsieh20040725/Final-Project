<!-- Back to top compatibility -->
<a name="readme-top"></a>

<!-- PROJECT BANNER -->
<!-- Optional if you have a banner -->
<!-- ![project_banner](https://your-image-link-here) -->

<h1 align="center">Flooded Area Classification using Sentinel-2 and NDWI + K-means</h1>
<p align="center">
  Using unsupervised learning and Sentinel-2 imagery to detect inland water bodies in flood-prone and dry regions.
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
        <li><a href="#remote-sensing-methods">Remote Sensing Methods</a></li>
        <li><a href="#machine-learning-method---k-means">Machine Learning Method – K-means</a></li>
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

# 📌 About the Project

This project is part of the GEOL0069 AI4EO module at University College London and focuses on the detection of surface water and flood presence using Sentinel-2 satellite imagery and unsupervised machine learning techniques. The goal is to detect and classify flooded vs. non-flooded areas in two hydrologically distinct regions:

- **Normalized Difference Water Index (NDWI)**
- **Modified NDWI (MNDWI)**
- **K-means clustering**

It compares the performance of these techniques in two contrasting regions:

- 🌍 **Khulna, Bangladesh** — a deltaic area prone to seasonal flooding  
- 🌏 **Mandalay Region, Myanmar** — a dry control region with minimal water change

The notebook evaluates how each approach performs in flood-prone vs. dry conditions, using open-access **Sentinel-2** data.
The project leverages the Normalized Difference Water Index (NDWI) and Modified NDWI (MNDWI) as remote sensing indicators, and compares these with machine learning outputs from K-means clustering using various Sentinel-2 band combinations.

Through this comparison, the project aims to evaluate the performance and transferability of water detection algorithms under different hydrological conditions. Emphasis is also placed on environmental efficiency by evaluating compute-related emissions using the codecarbon tool.



---

## 💡 Description of the Problem

Flooding is one of the most frequent and devastating climate-related hazards, impacting more than 1.5 billion people globally between 2000 and 2019 (UNDRR, 2022). Accurate flood detection is critical for disaster response, infrastructure protection, and humanitarian relief.

Traditional flood mapping relies on ground surveys or drone-based assessments, which are costly, time-intensive, and geographically limited. Satellite remote sensing provides a scalable alternative for flood detection, enabling large-area and near-real-time analysis.

This project addresses the problem of water detection across diverse environments, using freely available Sentinel-2 imagery and basic machine learning tools. It contrasts flooded and dry regions to explore:

- How well NDWI and MNDWI can detect water presence across different land types.
- Whether K-means clustering can match or improve on classic water indices.
- How band combinations affect water detection under varying spectral noise, such as urban shadows or sediment-laden rivers.

By applying both visual and quantitative analysis, this project aims to provide a robust comparison framework and demonstrate a lightweight, replicable approach to water mapping in data-scarce settings.


---

## 🌐 Background

Remote sensing is a powerful tool for environmental monitoring, offering wide-scale and repeated coverage without the need for field visits. In the context of flood and water detection, the Normalized Difference Water Index (NDWI) has long been used to highlight surface water using Green (B03) and NIR (B08) reflectance.

However, NDWI has notable limitations:

- It struggles in built-up or turbid areas due to spectral confusion.

- It can misclassify sediment-heavy floodwaters as land.

To address this, alternative indices like Modified NDWI (MNDWI) using Green (B03) and SWIR1 (B11) have been proposed, which suppress urban and vegetative reflectance and enhance water contrast (Xu, 2006).

This project builds on these foundations by:

- Comparing NDWI and MNDWI maps.

- Applying K-means clustering on multiple band pairs (NDWI, SWI, MNDWI).

- Analyzing how performance varies between the Khulna floodplain and Mandalay dryland.

The analysis demonstrates how simple unsupervised models, when paired with thoughtful band selection, can support efficient flood mapping even in challenging environments.



---

## 🛰 The SENTINEL-2 Satellite

Sentinel-2 provides global optical imagery at 10–60m resolution across 13 bands. For this project, we used:

| Band | Name         | Wavelength | Use                     |
|------|--------------|------------|--------------------------|
| B03  | Green        | 560 nm     | Water detection (NDWI)   |
| B08  | NIR          | 842 nm     | NDWI pairing             |
| B11  | SWIR1        | 1610 nm    | MNDWI + SWI methods      |
| B05  | Red Edge     | 705 nm     | SWI index for ML         |

These combinations are used to detect water presence, suppress noise from vegetation or built-up areas, and compare seasonal change.

![ee0a8264d27979fc5bd6f5bf1394407](https://github.com/user-attachments/assets/23f39a22-c7eb-485d-b23d-4122e22242a0)








---

## 🛰 Remote Sensing Methods

### NDWI (McFeeters, 1996)
```math

NDWI = \frac{Green - NIR}{Green + NIR}
```
Highlights water bodies, but can be confused by urban or shadowed regions.

### MNDWI (Xu, 2006)
```math

MNDWI = \frac{Green - SWIR1}{Green + SWIR1 + \epsilon}
```
Improves accuracy in built-up or turbid areas by replacing NIR with SWIR.
![9899d54a56ca45641a94e5328da6317](https://github.com/user-attachments/assets/45b9ab25-bdb0-4d40-9510-17ae353bc9f5)




---

## 🤖 Machine Learning Method – K-means

**K-means clustering** is used to classify each pixel based on spectral similarity — no labels or ground truth are required.

We apply it to:
- NDWI bands (B03 + B08)
- MNDWI bands (B03 + B11)
- SWI bands (B05 + B11)

It helps compare whether machine learning can match or outperform traditional NDWI detection.

### Workflow:
1. Load Sentinel-2 bands
2. Calculate NDWI / MNDWI
3. Apply threshold to create binary water mask
4. Run K-means on stacked bands (2D array)
5. Visualize and compare outputs



<p align="right">(<a href="#readme-top">back to top</a>)</p>


---

# 🚀 Getting Started

### Requirements:
- Python 3.8+
- Jupyter Notebook or Google Colab
- `rasterio`, `scikit-learn`, `numpy`, `matplotlib`, `codecarbon`

### How to Run:
1. Clone the repo
2. Upload Sentinel-2 `.SAFE` bands to Google Drive
3. Open the `.ipynb` file and change the file paths
4. Run cells in order — NDWI masks, K-means classifications, and comparison charts will be shown

---

## 📦 Datasets Used

**Sentinel-2 L2A** images were downloaded from the [Copernicus Dataspace Browser](https://dataspace.copernicus.eu/).

| Region            | Date Range   | Season         |
|------------------|--------------|----------------|
| Khulna, Bangladesh | March 2025   | Flood season   |
| Mandalay, Myanmar | March 2025   | Dry season     |

Only bands B03, B05, B08, and B11 were used. Images were downsampled for memory efficiency.

---

# ♻️ Environmental Cost

This project uses lightweight computation. No GPU, no training, just CPU-based inference + K-means.

Emissions were logged using `codecarbon`.

| Region     | Emissions |
|------------|------------|
| 🌍 Khulna   | 0.000055 kg CO₂ |
| 🌏 Mandalay | 0.000060 kg CO₂ |

> ⚠️ Compare this to a 2-hour car trip (0.5 kg CO₂): this is ~**4,000x lower**.

### Why so low?

- No field visits, drones, or travel
- Public satellite data
- Google Colab uses shared computing
- Downsampled raster files reduce processing load

> This aligns with sustainable AI goals for **low-carbon machine learning**  
> (Strubell et al., 2019; Lacoste et al., 2019)

---

# 🎥 Video Overview

A short walkthrough video is included, covering:
- NDWI & MNDWI generation
- K-means clustering implementation
- Visual comparisons
- Carbon emission logging

[🔗 Link to video once uploaded]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

# 📜 License

Distributed under the MIT License. See `LICENSE.txt` for details.

---

# 👤 Contact

**[Your Name]**  
University College London  
GEOL0069 – AI4EO  
[Your Email or GitHub]

---

# 📚 References

- McFeeters, S.K. (1996). NDWI for delineating open water. *IJRS*
- Xu, H. (2006). MNDWI for better water separation. *RSE*
- Jiang et al. (2020). SWI: Red edge + SWIR for water. *Remote Sensing Letters*
- Zeng et al. (2023). Review on water body detection. *Remote Sensing Reviews*
- EEA (2023). Average car trip emissions: https://www.eea.europa.eu
- Strubell et al. (2019). Energy & policy for deep learning. *ACL*
- Lacoste et al. (2019). Quantifying CO₂ in ML. *MLCO2.org*

<p align="right">(<a href="#readme-top">back to top</a>)</p>
