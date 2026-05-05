## 🏗️ Architecture

### Generator (Lightweight CycleGAN – 6 Residual Blocks)

The generator is the core component of the CycleGAN model and is responsible for learning the mapping between the two image domains: **sketches and photos**. It follows an **encoder–residual–decoder style architecture**, which allows the network to first compress the image into feature representations, transform those features, and then reconstruct the image in the target domain.

The input to the generator is a **128×128 RGB image**, which can either be a hand-drawn sketch or a real photo depending on the translation direction.

In the **encoding stage**, the network applies **two convolutional downsampling layers**. These layers gradually reduce the spatial dimensions of the image while increasing the number of feature channels. This helps the model learn meaningful hierarchical features such as edges, textures, and structural patterns.

After encoding, the network passes the compressed representation into the **transformation stage**, which consists of **6 Residual (ResNet) blocks**. These residual blocks are designed to improve learning stability and allow the network to preserve important structural information from the input image. Each residual block learns a small modification instead of rewriting the entire representation, which helps in producing more consistent and realistic outputs.

Once feature transformation is complete, the model enters the **decoding stage**, where it reconstructs the image back to its original resolution. This is done using **two transposed convolution (upsampling) layers**. These layers progressively increase the spatial dimensions while reducing feature depth, gradually rebuilding the image structure.

Finally, a **convolutional output layer with Tanh activation** is applied to generate the final output image. The Tanh activation scales pixel values between **-1 and 1**, which is standard practice in GAN-based image generation tasks.

The final output is a **128×128 RGB image**, which represents the translated result. Depending on the input direction, the generator performs:
- **Sketch → Photo translation**
- **Photo → Sketch translation (reverse mapping)**

Overall, this is a **simplified CycleGAN generator design**, optimized with fewer residual blocks to reduce computational cost while still maintaining the ability to learn meaningful cross-domain transformations.