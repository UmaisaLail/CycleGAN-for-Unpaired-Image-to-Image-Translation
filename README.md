## 🏗️ Architecture

### 🔷 Generator (Lightweight CycleGAN – 6 Residual Blocks)

The generator is the main component of the CycleGAN model, responsible for learning the mapping between two image domains: **sketches and photos**. It follows an **encoder–residual–decoder architecture**, where the image is first compressed into feature representations, then transformed in latent space, and finally reconstructed into the target domain.

The input to the network is a **128×128 RGB image**, which can be either a sketch or a real image depending on the translation direction.

---

### 🔹 Encoding Stage

In the encoding phase, the model applies **two convolutional downsampling layers**. These layers progressively reduce the spatial resolution while increasing the depth of feature channels.

This helps the model learn:
- Edge structures  
- Basic shapes  
- Texture-level features  
- High-level spatial patterns  

---

### 🔹 Transformation Stage

After encoding, the representation is passed through **6 Residual (ResNet) blocks**.

These blocks:
- Improve training stability  
- Preserve important spatial information  
- Learn small feature refinements instead of full transformations  
- Help maintain consistency in generated outputs  

---

### 🔹 Decoding Stage

The decoding stage reconstructs the image back to its original resolution using **two transposed convolution (upsampling) layers**.

These layers:
- Gradually increase spatial dimensions  
- Reduce feature depth  
- Restore fine visual details  

---

### 🔹 Output Layer

A final **convolutional layer with Tanh activation** generates the output image.

- Tanh scales pixel values to **[-1, 1]**
- This is commonly used in GAN-based image generation

---

### 🖼️ Output

The final output is a **128×128 RGB image**, representing the translated result.

Depending on the input direction, the model performs:

- Sketch → Photo translation  
- Photo → Sketch translation  

---

### 📌 Summary

This generator is a **lightweight CycleGAN variant**, designed to reduce computational cost while still maintaining strong image-to-image translation performance.
