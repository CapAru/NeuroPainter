# NeuroPainter
Grayscale to color image generator

---
## **Finalized Approach for Best Results**
### **1. Dynamic Resizing Without Resolution Loss**
- **Instead of resizing the original grayscale image permanently**, we:
  1. **Temporarily downscale** the image (e.g., 512x512) for processing.
  2. **Colorize it using a GAN** (trained on 512x512 images).
  3. **Upscale it back** to the original resolution using a Super-Resolution Model.

✅ **Pros:** No distortion, no fixed-size requirement, and high-quality results.

---

### **2. Step-by-Step Processing Pipeline**
#### **Step 1: Preprocessing**
- Convert image to **Lab color space** (keep L-channel).
- **Resize temporarily** (if the image is too large) for the GAN to handle.

#### **Step 2: Colorization with a GAN**
- Use a **U-Net or ResNet-based Generator**.
- Use **self-attention (SAGAN) for fine details**.
- Train on **higher resolution images (512x512 or more)**.
- The output will be a **512x512 colorized image**.

#### **Step 3: Super-Resolution for Scaling Up**
- Take the 512x512 colorized image.
- Use **ESRGAN or Real-ESRGAN** to **scale it back** to its original resolution.
- This **restores high-frequency details** and prevents resolution loss.

#### **Step 4: Merge & Output**
- Convert back to **RGB from Lab**.
- **Return the final colorized image** in the same resolution as the original grayscale input.

---

### **Why This Works Best**
✅ **Handles any resolution dynamically** – No fixed input size.  
✅ **No resolution decay** – Super-Resolution restores original quality.  
✅ **Realistic colors** – GAN learns high-quality colorization.  
