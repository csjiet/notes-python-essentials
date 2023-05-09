
What is a Binary Mask?
- Creating an array with 1 (white - image) being the area of interest, and 0 (black pixels - image) being the area ignored.
- ![[pixel_image_vs_mask.png | 300]]
> Image on the left, Binary mask on the right
- ![[image_after_binary_masking.png | 200]]

- Generating a Circular binary mask using Numpy array - using: `np.ogrid, <=`
```python
def create_circular_mask(h, w, center=None, radius=None):

    if center is None: # use the middle of the image
        center = (int(w/2), int(h/2))
    if radius is None: # use the smallest distance between the center and image walls
        radius = min(center[0], center[1], w-center[0], h-center[1])

    Y, X = np.ogrid[:h, :w]
    # Calculates distance of every point in the grid from the center point
    dist_from_center = np.sqrt((X - center[0])**2 + (Y-center[1])**2)

	# All distance from the center which is smaller than the radius will be True/ not masked.
    mask = dist_from_center <= radius
    return mask
```
> Notice, just like Desmos graphing, we can specify range to highlight using `inequalities` ($\le, <$)  to generate an area of interest.

- Generating a defined mask shape (e.g., circular) using CV2 - using: `cv2.bitwise_and()`
```python
import cv2
import numpy as np

# Load image, create mask, and draw white circle on mask
image = cv2.imread('1.jpeg')
mask = np.zeros(image.shape, dtype=np.uint8)
mask = cv2.circle(mask, (260, 300), 225, (255,255,255), -1) 

# Mask input image with binary mask
result = cv2.bitwise_and(image, mask)
# Color background white
result[mask==0] = 255 # Optional

cv2.imshow('image', image)
cv2.imshow('mask', mask)
cv2.imshow('result', result)
cv2.waitKey()
```

- Generating a mask with a specified color range from an image 
	- [] (https://www.tutorialspoint.com/how-to-mask-an-image-in-opencv-python)

Resources:
- [Manual creation of mask using Numpy arrays](https://stackoverflow.com/questions/44865023/how-can-i-create-a-circular-mask-for-a-numpy-array)
- [Image masking in CV2 with abstracted functions](https://stackoverflow.com/questions/59432324/how-to-mask-image-with-binary-mask)
