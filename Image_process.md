# Process images in Python (mainly for ".tiff/.tif").
## Package: [PIL](https://pillow.readthedocs.io/en/stable/index.html)/[OpenCV](https://pypi.org/project/opencv-python/)
## Modes that usually be used in reasearch: "I" "I;16" "I;16B"
## Load function:
      cv2.imread(file, cv2.IMREAD_MODE)

This returns a numpy array, size of [[channels, height, width](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html)].

      img = Image.open(file)
      img.convert("mode")
      img_array = np.array(img)
The first returns a [PIL object](https://pillow.readthedocs.io/en/stable/reference/Image.html), the second changes the image mode. Then it can be transfer to a numpy array. 

---
- **L (uint8, 0~255)**:
  
  The most common storage format of grayscale images. But it is rarely used for scientific research because the range of 0-255 is too small to carry enough information.
- **I (uint32, 0 ~ 2^31-1):**

  Using "Image.open(file).convert("I")" to load them.
- **I;16 (uint16, 0 ~ 65535):**

  When using "Image.open(file).convert()" to load this image, "convert("I;16")" will lead to wrong value. Pixel values greater than 32767 may be considered negative or wrap around. Using "convert("I")" is the best choice.Boundary value overflow occurs (65535 will become a negative or abnormally small value)
- **I;16B (uint16, 0 ~ 65535):**

  Usually represents a 16 bit unsigned integer (uint16) grayscale image, stored in **Big Endian** format. But don't be afraid, in OpenCV (cv2)/PIL, when reading 16 bit grayscale images (such as TIFF or PNG formats), byte order issues are usually automatically handled by OpenCV.
- **I;16SB (int16, -32768 ~ 32767):**

  Specific scientific applications allow negative values (such as certain image processing algorithms).
- **I;32F (float32, ):**

  Usually normalized to [0.0, 1.0], but can be any floating-point value.
- **I;64F (float64, ):**

  Usually normalized to [0.0, 1.0], but supports larger ranges. Usually used for advanced scientific computing and rarely for conventional image processing.
---
- **P (uint8, 0 ~ 255):**

  P mode is an 8-bit single channel image mode, where each pixel value is an 8-bit integer (range [0, 255]), but these values do not directly represent grayscale or color, but rather serve as an index pointing to a palette. A color palette is a color lookup table (LUT) that defines the actual RGB colors corresponding to each index.
