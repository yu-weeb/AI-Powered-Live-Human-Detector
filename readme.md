Link to Models:
https://drive.google.com/drive/folders/1tqtylyEl9Mxv-gyoAigldRZxanlapAgD?usp=sharing



Thermal Human Detection – YOLOv5 + Body-Part Ensemble
Overview-

This project performs real-time human detection on thermal images using a two-model YOLOv5 ensemble. Instead of relying on one detector, the system splits the task into:

Model 1 – Full Human Detector

Model 2 – Body-Part Detector (Head, Arm, Leg)

The goal is to improve robustness in cases where humans are partially visible, occluded, or low-resolution—common problems in thermal surveillance.

Why an Ensemble?

Thermal images usually lack fine details. A single detector often fails when:

The person is partially blocked

The body outline is faint

Only a head or leg is visible

By running two lightweight YOLOv5 models:

The full-body model catches normal, unobstructed detections.

The body-part model provides fallback detections when only small visible regions exist.

The system merges results so detection succeeds even under occlusion.

Models Used-

1. YOLOv5 (Human Detector)

Detects full person silhouettes

Trained on thermal images

Optimized for speed and low compute

2. YOLOv5 (Body Part Detector)

Predicts:

Head

Arm

Leg

Helps catch partial detections and improve tracking reliability

Both models are small, fast versions of YOLO (s/m) to keep resource usage low.

Optional: GAN-Based Inpainting

Thermal frames may have missing or blocked regions.
A GAN-based inpainting stage (e.g., DeepFill / GFPGAN) can be optionally applied before detection to:

Restore missing image sections

Improve bounding box accuracy

Reduce false negatives under heavy occlusion

This step is optional and can be toggled off for performance.

Pipeline-

Capture or load thermal frame

(Optional) Apply GAN Inpainting to fill corrupted regions

Run YOLOv5 Human detector

Run YOLOv5 Body-Part detector

Merge predictions using ensemble logic

Output visual detections

Training Details

Standard YOLOv5 training using thermal dataset (annotated)

Data augmentation: flips, noise, random masks

Custom anchor tuning for smaller body parts

Requirements-

Python 3.x

PyTorch

OpenCV

YOLOv5 environment

(Optional) GAN inpainting dependencies

Results-

Faster than heavy backbone detectors

More reliable in low-detail thermal conditions

Partial visibility no longer causes total detection failure


