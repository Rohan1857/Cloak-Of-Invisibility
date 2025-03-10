# Blue Cloak Effect

This project demonstrates a "Blue Cloak Effect" using OpenCV. The effect replaces blue regions in the video feed with a background image, creating an invisibility cloak effect. 

## Requirements

- Python 3.x
- OpenCV
- NumPy

## Installation

1. **Clone the repository:**

    ```sh
    git clone https://github.com/your-username/blue-cloak-effect.git
    cd blue-cloak-effect
    ```

2. **Install the required dependencies:**

    ```sh
    pip install numpy opencv-python
    ```

## Usage

1. **Run the script:**

    ```sh
    python blue_cloak_effect.py
    ```

2. **Instructions:**
   - The script will start capturing video from your default webcam.
   - It will take a few seconds to capture the background.
   - Make sure you have a blue object or cloth to see the effect.
   - Press `ESC` to exit the application.

## Code Explanation

```python
import numpy as np
import cv2
import time

# Capture video from the default webcam
cap = cv2.VideoCapture(0)
time.sleep(3)

# Capture the background frame
background = 0
for i in range(150):
    ret, background = cap.read()

# Flip the background frame
background = np.flip(background, axis=1)

while cap.isOpened():
    ret, img = cap.read()
    if not ret:
        break

    # Flip the current frame
    img = np.flip(img, axis=1)

    # Convert the image to HSV color space
    hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

    # Define the HSV range for blue
    lower_blue = np.array([90, 50, 50])
    upper_blue = np.array([130, 255, 255])

    # Create a mask for detecting blue color
    blue_mask = cv2.inRange(hsv, lower_blue, upper_blue)

    # Clean the mask using morphological operations
    mask = cv2.morphologyEx(blue_mask, cv2.MORPH_OPEN, np.ones((3,3), np.uint8), iterations= 10) 
    mask = cv2.morphologyEx(blue_mask, cv2.MORPH_DILATE, np.ones((3,3), np.uint8), iterations= 10)

    # Invert the mask to segment out non-blue areas
    mask_inverse = cv2.bitwise_not(mask)

    # Replace the blue regions with the background
    res1 = cv2.bitwise_and(background, background, mask=mask)

    # Retain the non-blue regions from the current frame
    res2 = cv2.bitwise_and(img, img, mask=mask_inverse)

    # Combine the two results 
    final_output = cv2.addWeighted(res1, 1, res2, 1, 0)

    # Display the result
    cv2.imshow('Blue Cloak Effect', final_output)

    # Exit on pressing ESC
    if cv2.waitKey(10) == 27:
        break

# Release the capture and destroy all windows
cap.release()
cv2.destroyAllWindows()
```

## License

This project is licensed under the MIT License.
