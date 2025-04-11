# **Brain Segmentation Model**
Developed by: [**Ashutosh Shukla**](https://www.linkedin.com/in/ashutosh-shukla4/)
## **Overview**
This notebook demonstrates a complete pipeline for converting 3D brain scans (from the Task01_BrainTumour dataset) into 2D top-view images using maximum intensity projection (MIP) and then training a 2D U-Net segmentation model with MONAI (v1.4.0), and finally performing inference on test images with automatic annotation of different brain regions. The regions are labeled with anatomical names (e.g., Grey Matter, White Matter, Hippocampus) according to a pre-defined mapping.
*   Due to low computational power, I converted the original 3D brain scans into 2D images. This significantly reduces the data complexity and computational requirements, enabling faster processing and model training.
* The conversion was done using **NiBabel** to load NIfTI files, and a **Maximum Intensity Projection (MIP)** along the Z-axis was applied to extract a top view of the brain.
* I chose the top view because it provides a clear overview of the brain's structure while reducing the data dimensionality.
