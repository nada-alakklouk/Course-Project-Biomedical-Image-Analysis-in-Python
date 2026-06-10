# 🫁 Biomedical Image Analysis: Cardiac MRI Left Ventricle Segmentation

A specialized Biomedical Engineering and Data Science project focusing on processing and segmenting 3D Magnetic Resonance Imaging (MRI) data from the **Sunnybrook Cardiac Dataset**. The primary clinical goal of this pipeline is to isolate the **Left Ventricle (LV)** from time-series cardiac frames, which is a critical precursor step for radiologists to compute the cardiac *Ejection Fraction* (the proportion of blood pumped out during each heartbeat).

---

## 📂 Project Structure & Assets

* 💻 **[View Core Analysis Notebook](./main.ipynb)** – Interactive Jupyter Notebook containing the full Digital Image Processing (DIP) and morphological pipeline.
* 📋 **Dataset Source:** Built using specialized DICOM imaging samples (`SCD2001_MR_117.dcm`) from the Sunnybrook Cardiac MRI dataset.

---

## 🛠️ Tech Stack & Advanced Libraries

* **Programming Language:** Python 🐍
* **Image Processing Toolsets:**
  * `imageio`: For parsing and reading complex healthcare-standard **DICOM** (`.dcm`) metadata and pixel arrays.
  * `scipy.ndimage` (`ndi`): For multi-dimensional gradient convolutions, mathematical morphology, and object labeling.
  * `numpy`: For high-performance matrix masking, element-wise filtering (`np.where`), and intensity transformations.
* **Visualization:** `matplotlib.pyplot` for rendering grayscale anatomical frames, intensity histograms, seismic edge maps, and dynamic color overlays.

---

## 🚀 Image Processing Pipeline & Methodology

The project implements an end-to-end medical vision workflow across the following key phases:

### 1. Medical Image Ingestion & Formatting
* Imported `.dcm` data, converted the structural array to `float64` precision, and leveraged customized colormaps (`cmap='gray'`, `vmin=0`, `vmax=255`) to visually amplify regional tissue contrast.

### 2. Geometric Transformations & Statistical Histograms
* Applied spatial interpolation filters to execute accurate pixel rotations (`ndi.rotate`).
* Computed voxel-intensity distributions and frequency histograms to scientifically define exact threshold margins.

### 3. Advanced Morphological Masking
* Formulated tissue masks isolating ranges of bone and muscle structure.
* Utilized morphological **Binary Dilation** and **Binary Closing** algorithms (`ndi.binary_closing`) to cleanly smooth jagged tissue margins and fill structural internal voids/holes.

### 4. Convolutions & Edge Detection
* Engineered a custom spatial weight kernel to perform discrete multi-dimensional convolutions (`ndi.convolve`), rendering sharp directional edge maps via a divergence-based `seismic` colormap.

### 5. Automated Object Segmentation & Bounding Box Extraction
* Applied a `median_filter` noise-reduction pass, labeled individual connected anatomical elements (`ndi.label`), and pinpointed the **Left Ventricle coordinates [128, 128]**.
* Dynamically extracted the structural bounding box using `ndi.find_objects` to seamlessly crop and isolate the left ventricle from the surrounding thoracic cavity.

---

## 📊 Visual Summary of Capabilities
* **DICOM Handling:** Direct native translation of raw clinical arrays.
* **Tissue Labeling:** Successfully indexed and categorized distinct internal regions (identified 26 discrete clusters).
* **Target Isolation:** Isolated the core cardiac region with sub-pixel precision bounding parameters: `(slice(107, 149), slice(116, 162))`.

---

## 👤 Developed by:
* **Nada Alaklook**
* 🔗 [Connect with me on LinkedIn](https://linkedin.com/in/nada-alaklook-725049252)
