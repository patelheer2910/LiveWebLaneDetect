# Real-time Lane Switching Optimization

## Executive Summary
We aim to develop an AI-Driven lane-switching optimization system that leverages real-time webcam footage and reinforcement learning. The model will track the vehicle density and movement in each lane on I-93, extracting key traffic patterns. A Deep Q-Learning (DQL) framework will then continuously predict the optimal lane to minimize travel time, adapting dynamically rather than making a one-time decision. 

## Project Description
**Project Title:** **AI-Driven Lane Switching Optimization Using Computer Vision and Reinforcement Learning**  

Efficient lane selection is critical for minimizing travel time and reducing highway congestion. Current traffic prediction models primarily focus on selecting the best lane at the start of a journey, but they lack adaptability to **real-time traffic dynamics**. This project proposes an AI-driven lane-switching optimization system that continuously predicts the **optimal lane** using **computer vision (CV) and reinforcement learning (RL)**.  

The system will leverage **real-time webcam feeds** from sources like Mass511 to extract lane-level traffic data. Using **YOLO** or **Mask R-CNN**, the model will detect and track vehicles, estimating their density, speed, and movement patterns per lane. This processed data will feed into a **Deep Q-Learning (DQL) model**, which will dynamically learn **when and where** to switch lanes based on real-time conditions. Unlike traditional models that rely on static traffic rules or fixed decision points, the proposed system will employ **adaptive decision-making**, continuously refining its strategy to ensure the shortest possible travel time.  

A key innovation in this project is the **combination of real-time vision-based lane assessment with reinforcement learning**. This hybrid approach will allow the model to adapt to sudden congestion shifts, aggressive driver behavior, and varying traffic flow conditions. The system will be evaluated based on metrics such as **average travel time reduction, lane-switching efficiency, and overall congestion impact**. By integrating **computer vision and RL**, this project aims to improve highway traffic flow, helping drivers make more informed and efficient lane-switching decisions.

## Goal 
The motive of this project is to develop a system that dynamically predicts the best lane for minimizing the travel time on I-93. This will be done to seel improved highway efficiency, reduced congestion-related delays, and enhanced driving decisions. 

## Data Collection
- **Source**: Utilize the [Mass511](https://mass511.com/) and other publicly available imformation covering diverse connecting routes to ensure model generalization.
- **Features**:
  -  **1. Computer Vision Features (From Webcam Feeds)**

     Using YOLO or Mask R-CNN, you can process live traffic camera footage to extract:

      - **Vehicle Density per Lane** – Number of cars in each lane.
      - **Vehicle Speed Estimation** – Tracking motion across frames to estimate speeds.
      - **Lane Occupancy Ratio** – Percentage of lane space occupied by vehicles.
      - **Vehicle Types & Sizes** – Detecting cars, trucks, motorcycles, and buses (which impact lane efficiency).
      - **Traffic Flow Patterns** – Identifying bottlenecks, sudden slowdowns, and                   congestion buildup.
      - **Brake Light Detection** – Sudden braking behavior indicating potential slowdowns.
  - **2. Real-Time Traffic Data (From Mass511 Reports)**
 
      - **Current Travel Speeds** – Average speed per highway segment.
      - **Traffic Incidents** – Accidents, roadwork, and congestion reports affecting lane             choice.
      - **Weather Conditions** – Rain, snow, fog, and visibility affecting lane speeds.
      - **Construction Zone Alerts** – Lane closures or diversions impacting lane                    availability.
  - **3. Time & Location-Based Features**
      - **Time of Day Traffic Trends** – Rush hour vs. off-peak traffic patterns.
      - **Day of the Week Impact** – Weekend vs. weekday congestion patterns.
      - **Special Event Proximity** – Nearby events that might influence traffic (e.g.,              sports games, concerts).
## Data Cleaning
- **1. Real-time Traffic Data (Webcam Feed)**
    - **a. Handlind missing frames or dropped data**
    - **b. Removing Blurry or Corrupted frames**
    - **c. Handling light and weather variations**
    - **d. Background subtraction and foreground extraction**
    - **e. Object detection and noise reduction**

- **2. Tabular Data from Mass511 Reports**
    - **a. Handling missing data**
    - **b. Standardizing format**
    - **c. Handling outliers**
    - **d. Dealing with redundant data**
    - **e. Encoding categorical data**

- **3. Time and Location-Based Features**
    - **a. Standardizing data**
    - **b. Incorporating special events**
    - **c. Handling anomalies in Traffic data**
    - **d. Real-time processing of data**

## Feature Extraction
- The extracted features will be transformed into structured data suitable for reinforcement learning.
- **Feature Representation for Reinforcement learning:**
    - Encoding lane states as numerical values for decision-making.
    - Defining state-action pairs for Deep Q-Learning based on extracted traffic attributes.
    - Implementing a reward system that penalizes congestion-prone decisions and incentivizes smooth traffic flow.



## Modelling
- **Model Architecture:** On a high level, our first step is to identify vehicles and analysis various attributes such as speed. Using this data, we will predict the best lane. For detection of vehicles, we will use **YOLO** or **Mask-R-CNN**. These algorithms will also estimate attributes such as speed, movement patterns, lane congestion, etc. All this combined data will be passed into a **Deep Q-Learning** model, to predict the best lane for the car to travel at a given time.
- **Training Approach:** Since the our model is based on reinforcement learning, we will establish a system of **punishments** and **rewards** to help the model get better at its estimates and predictions.


## Visualization
We plan to show a few graphs such as:
- Bar/line charts representing lane occupancy and vehicle speed over time. 
- Heatmaps showing lane-specific congestion levels over time.

Additionally, we will overlay predicted lane-switching actions on a video feed to compare model decisions with actual lane conditions.


## Test Plan / Metrics
We aim to ensure that our test data includes diverse traffic patterns (e.g., rush hour, adverse weather) to validate model generalization.

We will have several metrics, including:
- **Average Travel Time Reduction**: to measure the decrease in travel time compared to baseline strategies (e.g., static lane choice).
- **Lane-Switching Efficiency**:  to track the number of unnecessary lane switches and optimize for minimal switching while maintaining low travel time.
- **Congestion Detection Accuracy**:  to evaluate how accurately the model detects congestion and suggests appropriate actions.
- **Real-Time Performance**:  to measure latency in decision-making to ensure real-time adaptability.
- **Model convergence rate**: to assess the number of training iterations required for stable learning
