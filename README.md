# Workshop-1-Adding-Sunglasses-to-Your-Passport-Photo-Using-OpenCV

### Developed By: Navasri B
### Register No : 212225230196

## Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.
Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
Detects the face in an image.

Places a stylish sunglass overlay perfectly on the face.

Works seamlessly with individual passport-size photos.

Customizable for different sunglasses styles or photo types.

## Technologies Used:
Python

OpenCV for image processing

Numpy for array manipulations

## How to Use:
Clone this repository.

Add your passport-sized photo to the images folder.

Run the script to see your "cool" transformation!

## Applications:
Learning basic image processing techniques.

Adding flair to your photos for fun.

Practicing computer vision workflows

## PROGRAM:

```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceImage = cv2.imread('Nava_sri.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
```
faceImage.shape
```
```
#resized_faceImage.shape
faceImage.shape
```
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(250, 80))
print("image Dimension ={}".format(glassPNG.shape))
```
```
# Separate color and alpha channels
glassBGR = glassPNG[:, :, :3]
glassMask1 = glassPNG[:, :, 3]
```
```
# Display sunglasses and alpha mask
plt.figure(figsize=(12,5))

plt.subplot(121)
plt.imshow(glassBGR[:,:,::-1])
plt.title("Sunglasses")

plt.subplot(122)
plt.imshow(glassMask1, cmap="gray")
plt.title("Alpha Mask")

plt.show()
```
```

# Make a copy of the original face image
faceWithGlassesNaive = faceImage.copy()

# Resize sunglasses with background
glassResized = cv2.resize(glassBGR, (340, 95))

# Set glasses position
x = 330  # Slightly left
y = 300  # Slightly upward

# Get sunglasses dimensions
h, w = glassResized.shape[:2]

# Select face region
roi = faceWithGlassesNaive[y:y+h, x:x+w]

# Place sunglasses with original background
faceWithGlassesNaive[y:y+h, x:x+w] = glassResized

# Display medium-size photo
plt.figure(figsize=(5, 7))
plt.imshow(cv2.cvtColor(faceWithGlassesNaive, cv2.COLOR_BGR2RGB))
plt.title("Sunglasses Fitted")
plt.axis("off")
plt.show()
```

```


# Resize mask to match wider sunglasses
glassBGR = cv2.resize(glassBGR, (340, 80))
glassMask1 = cv2.resize(glassMask1, (340, 80),
                        interpolation=cv2.INTER_NEAREST)

# Create 3-channel mask
glassMask = cv2.merge((glassMask1,
                       glassMask1,
                       glassMask1))

# Convert mask values to 0 and 1
glassMask = np.uint8(glassMask / 255)

# Make a copy of face image
faceWithGlasses = faceImage.copy()

# EYE REGION COORDINATES
x = 330   # Slightly left to keep glasses centered
y = 300   # Same upward position

h = glassBGR.shape[0]
w = glassBGR.shape[1]

# Extract eye ROI
eyeROI = faceWithGlasses[y:y+h, x:x+w]

# Remove region where glasses will be placed
maskedEye = cv2.multiply(eyeROI, (1 - glassMask))

# Extract glasses using mask
maskedGlass = cv2.multiply(glassBGR, glassMask)

# Combine both images
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Replace eye region with combined image
faceWithGlasses[y:y+h, x:x+w] = eyeRoiFinal

# Intermediate Results
plt.figure(figsize=(12, 5))

plt.subplot(131)
plt.imshow(maskedEye[:,:,::-1])
plt.title("Masked Eye Region")

plt.subplot(132)
plt.imshow(maskedGlass[:,:,::-1])
plt.title("Masked Sunglass Region")

plt.subplot(133)
plt.imshow(eyeRoiFinal[:,:,::-1])
plt.title("Combined ROI")

plt.show()
```

```
# Final Result
plt.figure(figsize=(12,8))

plt.subplot(121)
plt.imshow(faceImage[:,:,::-1])
plt.title("Original Image")
plt.axis("on")

plt.subplot(122)
plt.imshow(faceWithGlasses[:,:,::-1])
plt.title("With Sunglasses")
plt.axis("on")

plt.show()
```

## OUTPUT :

### Original Face Image :

<img width="493" height="472" alt="image" src="https://github.com/user-attachments/assets/12ebd26d-0919-41f3-8c68-2f2e86ed62a7" />


### Sunglass Image:

<img width="611" height="325" alt="image" src="https://github.com/user-attachments/assets/d1f96f98-9d70-4b12-8bcc-1bbb7e78eeea" />


### Image Dimension:

<img width="842" height="192" alt="image" src="https://github.com/user-attachments/assets/b2d3bd33-2d2a-4dd5-8235-cb759b66ba27" />


### Image with Sunglass:

<img width="432" height="521" alt="image" src="https://github.com/user-attachments/assets/211ff0ee-7b18-40f9-b517-44dc192356c4" />


### Augumented Eye and Sunglasses:

<img width="847" height="120" alt="image" src="https://github.com/user-attachments/assets/1e993387-5fb4-4967-995a-4e4afc731808" />


### Image with and without sunglasses:

<img width="863" height="502" alt="image" src="https://github.com/user-attachments/assets/a6991811-987d-4622-a00c-412545b02365" />


## RESULT:
Thus, the Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing has been done and verified successfully.

