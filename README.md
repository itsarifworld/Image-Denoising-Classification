# 🖼️ Image Denoising & Classification

This project implements an **Autoencoder-based image denoising pipeline** along with a **CNN classifier** to demonstrate how denoising improves classification performance.  
The entire project was developed and trained on Google Colab.

---

## Project Workflow

1. **Dataset Preparation**
   - Mounted Google Drive and used separate folders for:
     - `train/noisy`
     - `train/clean`
     - `test/noisy`
     - `test/clean`
   - Loaded noisy–clean pairs (X → noisy, Y → clean).
   - Normalized pixel values to range `[0, 1]`.

2. **Denoising Model**
   - Used a **Convolutional Autoencoder**:
     - Encoder: `Conv2D + MaxPooling`
     - Decoder: `UpSampling2D + Conv2D`
   - Loss function: `MSE`  
   - Optimizer: `Adam`

3. **Evaluation**
   - Denoising performance measured using:
     - **PSNR (Peak Signal-to-Noise Ratio)**
     - **SSIM (Structural Similarity Index)**

4. **Classification**
   - After denoising, built a **CNN classifier** for image recognition.
   - Compared accuracy on:
     - **Noisy images**
     - **Denoised images**

---

## 📊 Results

| Metric | Noisy Images | Denoised Images |
|--------|--------------|-----------------|
| PSNR   | ~7.8 dB      | ~9.0 dB         |
| SSIM   | 0.01         | 0.14            |
| Classifier Accuracy | Lower | Improved |

Even though the PSNR/SSIM look small, the denoised images visibly improved and boosted classification accuracy.

---

## Challenges I Faced (and What I Did)

1. **Dataset pairing was tricky**  
   - Problem: Making sure each noisy image matched the correct clean image.  
   - What I did: Wrote a loader that ensured `(X_noisy → Y_clean)` pairs were aligned before training.  

2. **Tensor shape mismatches in Autoencoder**  
   - Problem: Model crashed due to inconsistent sizes after pooling/upsampling.  
   - What I did: Carefully tracked input-output dimensions, adjusted filter sizes, and added padding.  

3. **Low PSNR/SSIM values confused me**  
   - Problem: Thought my model was failing since values were very small.  
   - What I did: Researched and learned that even small increases are meaningful in denoising.  

4. **Colab runtime crashes (memory/GPU limits)**  
   - Problem: Large dataset caused frequent disconnections.  
   - What I did: Resized images, used smaller batches, and saved intermediate checkpoints.  

5. **Training instability (loss not converging)**  
   - Problem: Model loss oscillated and didn’t improve.  
   - What I did: Lowered the learning rate, normalized inputs, and added dropout.  

---

## Key Learnings
- Autoencoders can clean images enough to significantly help downstream classifiers.  
- Evaluation metrics matter more than just visual inspection.  
- As a beginner, experimenting and failing taught me more than copying code.
