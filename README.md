# Project Description

## YouTube Link 
Find our Mid Term Presentation here: [Real-time Lane Traffic Detection](https://youtu.be/Md70Tk-DUI0?si=oH_1ATKJvD3yRhl-)

## Overview
This project aims to estimate real-time traffic density using YOLOv8, a state-of-the-art object detection model. By processing video frames or images, the system identifies and counts vehicles in different lanes to determine traffic intensity levels. This approach is beneficial for traffic management, congestion analysis, and urban planning by providing actionable insights into road usage patterns.

## Data Collection
This project aims to estimate real-time traffic density using YOLOv8, an object detection model. By processing video frames or images, the system identifies and counts vehicles in different lanes to determine traffic intensity levels. This approach is beneficial for things like traffic management, congestion analysis, and urban planning.

### Dataset Structure
- **Topview Vehicle Detection Image Dataset** from Kaggle<br>

  <img src="images/DataInfo.png" alt="Traffic Density" width="500"/>

## Data Processing

- **Frame Filtering**: The system preprocesses video frames by filtering out those that are blurry, contain excessive noise, or are corrupted due to camera malfunctions or adverse weather conditions.
- **Region of Interest (ROI) Selection**: To improve accuracy, the model focuses on specific lanes by masking out irrelevant areas, ensuring that only the relevant traffic regions are analyzed.
- **Background Subtraction**: Moving vehicles are isolated from the static background to enhance detection accuracy. This step ensures that stationary objects such as road signs and traffic lights do not interfere with vehicle detection.

## Data Modelling
We are using YOLOv8n, aka YOLOv8 Nano, which is a version of the YOLOv8 family designed for speed and resource efficiency.
### Model Architecture
- **Backbone**: CSPDarkNet (Cross Stage Partial Darknet) for feature extraction.
- **Neck**: PAN (Path Aggregation Network) for fusion of features.
- **Head**: YOLOv8 detection head for anchor-free design.

### Training Process
- **Hyperparameters**:<br>

  <img src="images/modelParameters.png" alt="Traffic Density" width="500"/>

- **Loss Functions**:
  - **Box Loss**: Measuring bounding box regression accuracy.
  - **Classification Loss**: Measures class prediction accuracy.
  - **Distribution Focal Loss**: Handling class imbalance.

### Model Evaluation
- **Key Metrics**:
  - **Precision**: Ratio of TP to positive predictions.
  - **Recall**: Ratio of TP to all actual predictions.
  - **mAP@0.5**: Mean Average Precision at IoU threshold of 0.5.
  - **mAP@0.5:0.95**: Mean Average Precision across IoU threshold of 0.5 to 0.95.

## Vehicle Detection and Lane Identification
We identify vehicles within each frame using YOLO. We first isolate the region of interest (ROI) in the frame, typically focusing on the lanes of interest, using a mask to eliminate irrelevant areas. This can be done by blacking out the regions outside the specific vertical range of the lanes, ensuring that only the lanes are considered for vehicle counting.
<br>

  <img src="images/Detections.png" alt="Traffic Density" width="500"/>
After applying the detection model, bounding boxes are drawn around the vehicles, and their characteristics—such as size, position, and movement—are extracted. These boxes are then used to track vehicle movements, which helps estimate vehicle speeds and lane occupancy.
<br>

  <img src="images/LaneDetects.png" alt="Traffic Density" width="500"/>
  
## Traffic Density Estimation
The system calculates the number of vehicles in each lane based on detected bounding boxes.

- **Traffic density is estimated by a predefined threshold of 10 for vehicle counts**:
  - **High vehicle count**: The lane is classified as having "Heavy" traffic.
  - **Low vehicle count**: The lane is classified as having "Smooth" traffic.
- The system continuously updates traffic density estimations in real-time as new frames are processed.
- The density estimation algorithm ensures minimal errors by filtering out false detections and considering factors like vehicle occlusion and lighting conditions.

## Real-Time Feedback
The system processes video frames dynamically, providing real-time updates on traffic density.

- A dashboard or interface can display:
  - Real-time bounding box visualization of detected vehicles.
  - Lane-wise vehicle counts for easy traffic assessment.
  - Current traffic intensity classification for each lane.
- Data visualization tools such as Matplotlib and OpenCV assist in interpreting traffic patterns and trends over time.
- The system can be integrated with traffic control centers to trigger alerts for congestion-prone areas, allowing for better traffic management and planning.

## Preliminary Results
<br>

  <img src="images/DetectPredictions.jpg" alt="Traffic Density" width="500"/>

After fine-tuning, the YOLOv8 model got better at predicting correct classes for the images (highlighting vehicles detected with bounding boxes) in a large variety of different scenarios – multiple camera views, different types of roads, varying traffic and lighting conditions.
<br>

  <img src="images/lossPlots.jpg" alt="Traffic Density" width="500"/>

- The loss curves (box loss, classification loss, and distribution focal loss) show that the learning is effective and there is no overfitting.
- Precision and recall are stable at approximately 0.9, showing that the model is identifying vehicles with high accuracy.
- mAP50, mAP50-95 show that the model is performing strongly and is reliable across multiple confidence thresholds.

### Confusion Matrix
<br>

  <img src="images/ConfusionMatrix.jpg" alt="Traffic Density" width="500"/>

- The normalized confusion matrix shows a strong true positive rate of **0.98** for vehicle detection and **1.00** for correctly classifying background elements.
- There is a minimal false negative rate (0.02) where vehicles are incorrectly classified as background.
- The negligible false positive rate confirms the model rarely misidentifies background elements as vehicles, which is crucial for accurate traffic density estimation.

### F1 Confidence Curve
<br>

  <img src="images/F1_curve.jpg" alt="Traffic Density" width="500"/>

- The graph shows the F1 Confidence curve for the classes.
- The optimal **F1 score is 0.93 at a confidence threshold of 0.502**.
- The curve maintains high F1 scores (above 0.8) across a wide range of confidence thresholds (approx. 0.1 - 0.8), indicating robustness and consistency for real-world deployment scenarios.
