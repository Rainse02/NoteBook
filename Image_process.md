# Process GrayScale images in Python (only for ".tiff/.tif").
## Package: PIL/CV
## Modes that usually be used in reasearch: "I" "I;16" "I;16B" "L"
- **"L" (uint8, 0~255)**:
  
  The most common storage format of GrayScale images. But it is rarely used for scientific research because the range of 0-255 is too small to carry enough information.
- **"I" (uint32, 0 ~ 2^31-1)**:

  
- **"I;16" (uint16, 0 ~ 65535)**:

  When using "cv2.imread()" to load this image, 
- **"I;16B" (uint16, 0 ~ 65535)**:
