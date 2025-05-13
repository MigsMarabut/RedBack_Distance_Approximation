# Depth Estimation and Distance Approximation using Computer Vision

![Readme style: standard](https://img.shields.io/badge/readme%20style-standard-brightgreen)
![Python](https://img.shields.io/badge/Python-3.10-blue)

## Overview

This project uses computer vision techniques to approximate distances within a single image by leveraging depth estimation and object detection models. The broader goal is to create an accessible, lightweight alternative to LiDAR or stereo vision for applications like assistive technologies or robotics—particularly for scenarios with constrained hardware (e.g., using only a single RGB camera).

We estimate the spatial position of objects from a monocular image and visualize potential danger zones based on distance brackets.

## Models Used

### Object Detection

A pre-trained model from Roboflow (COCO-style dataset) is used for identifying key objects in the image.

- [COCO Detection Model](https://universe.roboflow.com/microsoft/coco/model/37)

### Depth Estimation

We use the HuggingFace-hosted `Depth-Anything` pipeline, which returns a pixel-wise depth map from a single image.

- [Depth Anything V2](https://depth-anything-v2.github.io/)

## How it Works

1. **Image Input**: Load a static image (e.g., from the DIODE dataset).
2. **Object Detection**: Identify and label key objects using Roboflow model.
3. **Depth Estimation**: Use `Depth Anything V2` to generate a depth map.
4. **Distance Bracketing**: Convert the depth map into distance brackets and generate region overlays to visualize proximity.
5. **Visualization**: Overlay both the detections and spatial danger zones onto the image.

## Example Visualizations

- ![image](https://github.com/user-attachments/assets/ba46a8a0-125c-4e82-8721-c82fc2088aa4)

  *Boundary Detection*

- ![image](https://github.com/user-attachments/assets/97000b8b-ea36-4861-8780-33069dd68f4a)
  *Estimated depth*

- ![image](https://github.com/user-attachments/assets/a4cd78a4-9bef-40ac-97c3-66fc1848f3d8)

  *Detected objects with danger zones visualized*
- ![image](https://github.com/user-attachments/assets/d5a33d6b-c597-448d-b693-5db3c3a66e3c)

  *Global danger level: MID  | worst direction: LEFT  | min depth: 1.76 m*


> Note: The above images are placeholders. Replace with your outputs if hosting images in GitHub or Imgur.

## Code Flow Summary

```python
# Load image and estimate depth
image = Image.open("test1.jpg")
depth = pipe(image)["depth"]

# Use Roboflow inference model to get detections
results = model.infer(image)

# Visualize depth-based brackets and annotate danger zones
