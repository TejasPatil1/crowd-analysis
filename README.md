# Crowd Detection and Density Estimation

This project uses computer vision to detect people in images and estimate how they are distributed across a given area.

## Approach

The project uses a pretrained **RT-DETR (Real-Time Detection Transformer)** model for person detection. The model is loaded using Hugging Face Transformers and is used to identify people in input images.

The main steps are:

1. **Person Detection**
   RT-DETR detects people in the image and returns their bounding boxes along with confidence scores.

2. **Confidence Filtering**
   Detections are filtered using a confidence threshold to remove low-confidence results.

3. **Foot Point Extraction**
   The bottom-center point of each bounding box is taken as the approximate position of a person on the ground.

4. **Perspective Transformation**
   OpenCV's homography transformation is used to convert image coordinates into real-world venue coordinates.

5. **Zone Mapping**
   The projected positions are mapped to predefined areas of the venue to calculate the number of people in each zone.

## Model and Libraries

* **RT-DETR** – Person detection
* **Hugging Face Transformers** – Loading and running the pretrained model
* **OpenCV** – Image processing and perspective transformation
* **NumPy** – Coordinate calculations
* **Python** – Implementation

## Detection Pipeline

```text
Input Image
    ↓
RT-DETR Person Detection
    ↓
Confidence Filtering
    ↓
Bounding Box Extraction
    ↓
Foot Point Calculation
    ↓
Homography Transformation
    ↓
Real-World Coordinates
    ↓
Zone-wise Crowd Distribution
```

## Model Details

The project uses the pretrained `PekingU/rtdetr_r50vd` model with the Hugging Face `RTDetrForObjectDetection` implementation.

Only the person class is considered for detection. The model is used directly without additional training or fine-tuning.

## Coordinate Mapping

Four reference points on the ground plane are used to calculate a homography matrix. This matrix maps points from the camera image to the corresponding positions in the venue layout.

The transformed coordinates are then used to determine how people are distributed across different zones.

## Project Focus

The main computer vision concepts used in this project are:

* Object detection using RT-DETR
* Bounding box processing
* Image-to-world coordinate transformation
* Homography and perspective mapping
* Spatial crowd distribution analysis
