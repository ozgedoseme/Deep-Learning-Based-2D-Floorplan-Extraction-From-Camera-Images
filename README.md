# Deep-Learning-Based-2D-Floorplan-Extraction-From-Camera-Images

> **B.Sc. Graduation Project (2025-2026 Academic Year)**  
> **Institution:** Ege University, Faculty of Engineering, Department of Electrical and Electronics Engineering  
> **Authors:** Özge Döşeme ([dosemeozge48@gmail.com](mailto:dosemeozge48@gmail.com)), Görkem Tokoğul ([gorkemtokogul88@gmail.com](mailto:gorkemtokogul88@gmail.com)) 
> **Project Advisor:** Assoc. Prof. Dr. Erkan Zeki Engin ([erkan.zeki.engin@ege.edu.tr](mailto:erkan.zeki.engin@ege.edu.tr))  

---

## Abstract

This project aims to extract spatial geometry from 360° panoramic indoor images and generate two-dimensional floor plans using deep learning-based methods. Traditional indoor floor planning often relies on manual measurements or expensive hardware sensors. To address these limitations in time, cost, and accessibility, this study proposes a low-cost, scalable, and automated deep learning solution. 

Utilizing the **HorizonNet** architecture, the model predicts ceiling-wall and floor-wall boundaries from equirectangular panoramas. By processing both synthetic data **(Structured3D)** and real-world complex indoor data **(ZInD)**, the system generates metric-scale 2D room layouts and aligns individual rooms using camera pose parameters to construct a complete house floor plan.

---

## Aim & Scope

- **Digital Transformation:** Provide a fast, low-cost, digital alternative to manual indoor mapping and high-cost hardware.
- **Core Methodology:** Predict 360° room boundaries, project 3D geometry into 2D room layouts, and align multiple rooms using global coordinate transformations.
- **Key Applications:** Architectural documentation, indoor navigation, smart home mapping, and spatial planning.

---

## Methodology & Pipeline

The project workflow follows four main stages:

### 1. Literature Review & Dataset Selection
- **HorizonNet Framework:** Takes a single 360° RGB equirectangular panorama as input and predicts column-wise ceiling/floor boundaries and corner locations under the **Manhattan World assumption**.
- **Structured3D Dataset (Synthetic):** ~3,500 panoramas used. Labels were extracted directly from raw JSON files using a custom-developed parsing algorithm.
- **ZInD Dataset (Real-World):** ~12,000 panoramas across ~500 complex homes, providing real-world diversity and evaluation capability.

### 2. Model Training & Optimization
- Data split into Training, Validation, and Test sets.
- Optimized using batch sizes of `8` and `16`, alongside gradual learning rate decay to refine room corner predictions.

### 3. Generation of 2D Room Plans
- Derived UV-based room boundary points from HorizonNet outputs.
- Calculated point distances using camera z-components and ceiling heights to determine physical room dimensions.
- Generated room boundary polygons, calculating precise wall lengths and metric room areas.

### 4. Generation of Complete House Floor Plan
- Extracted rotation and translation parameters of cameras from JSON.
- Transformed room geometries into a global real-world coordinate system (rotation for correct orientation alignment; translation for precise spatial positioning).

---

## Experimental Results & Performance

The model achieved high agreement with ground truth data, obtaining an **Intersection over Union (IoU) rate exceeding 90%** in most test cases.

### Dataset Performance Comparison

| Metric / Parameter | ZInD Dataset (Real-World) | Structured3D Dataset (Synthetic) |
| :--- | :---: | :---: |
| **Panoramic Images** | 12,000 | 3,500 |
| **Epochs Trained** | 72 | 60 |
| **Batch Size** | 16 | 16 |
| **Train/Total Loss** | 0.36 | 0.31 |
| **Valid/Total Loss** | 0.38 | 0.35 |
| **Valid 2D IoU** | **0.88** | **0.91** |
| **Valid 3D IoU** | **0.87** | **0.89** |
| **Valid $\delta_1$ ($\delta < 1.25$)** | **0.97** | **0.97** |
| **Valid RMSE** | 0.14 | 0.09 |

---

## Future Work

- **Automatic Camera Alignment:** Develop algorithms to estimate camera rotation and translation automatically without relying on dataset JSON.
- **Corner Error Reduction:** Investigate optimization methods to further reduce corner coordinate error (currently down to 0.3).
- **Non-Manhattan Support:** Extend the model beyond 90-degree wall assumptions to support non-orthogonalwalls.
- **Architectural Element Detection:** Incorporate object detection pipelines to identify doors, windows, and structural fixtures for detailed floor plans.

---

## Citation & References

This project builds upon the foundational architecture proposed by **HorizonNet**. If you use or reference this methodology, please acknowledge the original work:

- **Original Repository:** [sunghoonim/HorizonNet](https://github.com/sunghoonim/HorizonNet)

---

## Acknowledgements

We express our deepest gratitude to our thesis advisor, **Assoc. Prof. Dr. Erkan Zeki Engin**, for his invaluable guidance, technical insights, and continuous support throughout this project.
