# **Brain Segmentation Model**
Developed by: [**Ashutosh Shukla**](https://www.linkedin.com/in/ashutosh-shukla4/)
## **Overview**
This notebook demonstrates a complete pipeline for converting 3D brain scans (from the Task01_BrainTumour dataset) into 2D top-view images using maximum intensity projection (MIP) and then training a 2D U-Net segmentation model with MONAI (v1.4.0), and finally performing inference on test images with automatic annotation of different brain regions. The regions are labeled with anatomical names (e.g., Grey Matter, White Matter, Hippocampus) according to a pre-defined mapping.
*   Due to low computational power, I converted the original 3D brain scans into 2D images. This significantly reduces the data complexity and computational requirements, enabling faster processing and model training.
* The conversion was done using **NiBabel** to load NIfTI files, and a **Maximum Intensity Projection (MIP)** along the Z-axis was applied to extract a top view of the brain.
* I chose the top view because it provides a clear overview of the brain's structure while reducing the data dimensionality.
## **1. Dependencies and Environment Setup**
Let us begin by installing the required packages:

MONAI v1.4.0: A deep learning framework specifically for medical imaging.
nibabel: For reading NIfTI files.
opencv-python: For image processing and visualization.
PyTorch: For building and training the model.
## **2. Setting up Directory Structure and Data Paths**
* Data Paths:
The training (imagesTr, labelsTr) and testing (imagesTs) directories are defined.

* 2D Conversion Directories:
Separate directories are created for the converted 2D images and labels.
## **3. Converting 3D Volumes to 2D Top-View Images**
* Method:
Maximum intensity projection (MIP) is applied along the Z-axis to obtain a 2D image from each 3D volume.
## **4. Building Data Dictionaries**
* Train Data Dictionary
* Test Data Dictionary
## **5. Define Transforms and DataLoaders**
### **Training and Testing Transforms**
* LoadImaged: Loads images and labels from file paths.
* LambdaD: Converts images to grayscale (if needed) and adds a channel dimension.
* ScaleIntensityd: Normalizes the image intensity.
* Resized: Resizes images and labels to 256×256.
* RandRotateD: Applies random rotation augmentation.
* ToTensord: Converts the arrays into PyTorch tensors.
### **Train Transforms**
### **Test Transforms**
## **6. Define the 2D U-Net Model, Loss, and Optimizer**
* Model Configuration:
The 2D U-Net is defined for images with 1 channel and outputs 4 classes. DiceLoss is used for segmentation, and the Adam optimizer is applied.
## **7. Training Loop**
* Training Process:
The model is trained for 10 epochs, processing each batch from the training DataLoader, computing the Dice loss, and updating model parameters.
## **8. Inference and Automatic Region Annotation on Testing Data**
### **Automatic Annotation:**

* Model Prediction:
The trained model takes test image and produces segmentation mask—an array where each pixel is assigned a numeric label corresponding to a brain region.

* Mapping Numbers to Names:
I used a predefined dictionary (called region_names) to translate these numbers into human-readable labels (e.g., 1 = "Grey Matter", 2 = "White Matter", 3 = "Hippocampus").

* Extracting and Drawing Contours:
The code identifies the boundaries (*contours*) of each region in the segmentation mask—similar to drawing an outline around shapes on a page.

* Overlay and Annotation:
These contours are then drawn on the original image in distinct colors, and the region names are added as text at the center of each outlined area.



This project demonstrates an end-to-end pipeline for brain segmentation using 2D representations derived from 3D datasets. Due to current computational constraints, I converted the original 3D brain scans into 2D top-view images using a maximum intensity projection (MIP) method. This helped me for efficient training and testing with a 2D U-Net model, enabling rapid experimentation and meaningful segmentation of critical brain regions such as Grey Matter, White Matter, and Hippocampus.

Future Work:
With access to more robust computational resources, future work will extend this pipeline to directly handle full 3D datasets. This would involve:

* Leveraging 3D U-Net Architectures: Training and fine-tuning 3D segmentation models to capture volumetric context and complex spatial relationships inherent in brain scans.
* Advanced Data Augmentation & Preprocessing: Applying sophisticated augmentation techniques and improved normalization methods tailored for 3D medical images.
* Uncertainty Quantification: Integrating statistical analysis tools for uncertainty estimation, which can enhance diagnostic confidence.
* Atlas-Based Segmentation: Utilizing brain atlases to improve the anatomical labeling accuracy and enable more detailed region-specific analysis.

#### Building this have greatly enhanced my understanding of medical image analysis and deep learning, and I look forward to further exploring these challenges with improved computational power and resources in the future.

#### Please do let me know about your reviews and feedbacks.
### Connect with me on [**LinkedIn**](https://www.linkedin.com/in/ashutosh-shukla4/)



