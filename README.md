# Invisibility Cloak

This project demonstrates an “Invisibility Cloak” effect using OpenCV. The script makes objects of a specific color (blue in this case) blend seamlessly with a captured background, creating a live “invisibility” illusion.

## Features
1. Captures background frames for a few seconds.  
2. Detects a color range (blue) in the video feed.  
3. Replaces the detected color with the previously captured background.  
4. Demonstrates a live invisibility effect.

## Requirements
• Python 3.x  
• OpenCV (cv2)  
• NumPy  

You can install the required dependencies with:
```bash
pip install opencv-python numpy
```

## Usage
1. Connect a webcam or ensure one is available.  
2. Execute the Python script:
```bash
python invisibility_cloak.py
```  
3. Stand in front of the camera with a blue cloth (or wear a blue garment).  
4. Press the ESC key to exit the application.

## Explanation of Key Steps
• Capture the background frames:  
  The script waits a few seconds, capturing multiple frames and storing one as the background.  

• Mask generation with HSV color space:  
  The frames are converted to the HSV color space, and a mask is created to isolate the specified color range.  

• Morphological operations:  
  Morphological opening and dilation clean up the mask by removing noise and filling holes.  

• Combining frames:  
  The final image is produced by combining the areas from the background and the current frame, effectively hiding the blue region.

## License
Feel free to use and modify this project under the MIT License.
