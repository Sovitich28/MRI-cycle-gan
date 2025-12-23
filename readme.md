# Brain MRI Style Transfer with CycleGAN

This project implements a style transfer application for Brain MRI images using CycleGAN. It allows users to convert MRI images between T1-weighted and T2-weighted styles.

## Features
- **T1 to T2 Conversion**: Transform T1-weighted MRI images into T2-weighted style.
- **T2 to T1 Conversion**: Transform T2-weighted MRI images into T1-weighted style.
- **User-Friendly Interface**: Built with Streamlit for easy image uploading and visualization.
- **Real-time Inference**: Uses pre-trained Keras models for fast style transfer.

## Notebook Workflow (`T2_T1_MRI_GAN.ipynb`)

The Jupyter notebook included in this repository details the complete process of building and training the CycleGAN model:

1.  **Problem Statement**: The goal is to generate artificial MRI images of different contrast levels (T1 to T2 and vice versa) using a Generative Adversarial Network (GAN).
2.  **Data Loading & Visualization**:
    -   Loads T1 and T2 MRI datasets.
    -   Visualizes sample images from both domains.
3.  **Data Preprocessing**:
    -   Normalizes image pixel values to the range [-1, 1].
    -   Resizes images to 64x64 dimensions.
    -   Batches and shuffles the data for training.
4.  **Model Architecture**:
    -   **Generator**: A modified U-Net architecture with skip connections and Instance Normalization.
    -   **Discriminator**: A PatchGAN discriminator to classify real vs. fake images.
5.  **Loss Functions**:
    -   **Adversarial Loss**: To ensure generated images look real.
    -   **Cycle Consistency Loss**: To ensure that translating an image to the other domain and back yields the original image ($T1 \to T2 \to T1 \approx T1$).
    -   **Identity Loss**: To ensure the generator preserves the image if it's already in the target domain.
6.  **Training**:
    -   The model is trained for 300 epochs.
    -   Checkpoints are saved during training.
    -   Generated images are visualized at each epoch to track progress.

## Training Progress
Below is a visualization of the training progress over epochs:

![Training Progress](DSC43_animated_cycleGAN_100_epochs.gif)

## Screenshots

### T1 to T2 Conversion
![T1 to T2 Conversion](t1%20to%20t2.PNG)

### T2 to T1 Conversion
![T2 to T1 Conversion](t2%20to%20t1.PNG)

## Project Structure
- `app.py`: The main Streamlit application script.
- `generator_t1_to_t2.keras`: Pre-trained model for T1 to T2 style transfer.
- `generator_t2_to_t1.keras`: Pre-trained model for T2 to T1 style transfer.
- `requirements.txt`: List of Python dependencies.
- `T2_T1_MRI_GAN.ipynb`: Jupyter notebook containing the training logic and model development.
- `cyclegan_mri.gif`: GIF showing the training evolution.

## Installation

1. Clone the repository or extract the project files.
2. Install the required dependencies using pip:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. Run the Streamlit application:
   ```bash
   streamlit run app.py
   ```
2. Open your web browser and navigate to the URL provided by Streamlit (usually `http://localhost:8501`).
3. Upload a Brain MRI image (PNG or JPG).
4. Select the desired transfer direction (T1 → T2 or T2 → T1).
5. View the input and the style-transferred output side-by-side.

## Technical Details
The project uses a CycleGAN architecture with a U-Net based generator. Images are preprocessed to 64x64 grayscale before being passed through the generator and then post-processed back to their original size for display.

---
