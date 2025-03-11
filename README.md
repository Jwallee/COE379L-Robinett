# COE 379L: Software Design For Responsible Intelligent Systems

This repository contains multiple projects developed for the **COE 379L** course at The University of Texas at Austin.  
The projects focus on data processing, machine learning, and neural network-based image classification, culminating in the deployment of a model using an inference server. Each project folder containes individual write-ups if more detial is needed.

## Projects

### **Project 1: Exploratory Data Analysis and Data Processing**
- Performed data exploration and preprocessing.
- Applied Linear Regression on processed data to identify trends and relationships.

### **Project 2: Machine Learning Classification Techniques**
- Implemented multiple **classification algorithms**, including:
  - K-Nearest Neighbor (KNN)
  - Random Forest Classifier
  - Decision Trees
  - Naive Bayes
  - Logistic Regression
- Evaluated model performance across datasets.

### **Project 3: Neural Networks for Image Classification**
- Developed a neural network model for image classification.
- Implemented a RESTful inference server to serve the trained model over HTTP.
- Dockerized the server, allowing deployment in a containerized environment.
- Exposed **two API endpoints**:
  1. **`/info`** - Returns metadata about the model and server status.
  2. **`/classify`** - Accepts binary image data and returns a **JSON classification result**.

### **Project 4: Airbnb Price Prediction Using Images**
- Designed a machine learning model to predict Airbnb listing prices based on image inputs.
- Utilized computer vision techniques to analyze property images and estimate an accurate price range.
- Explored the feasibility of using image-based valuation for real estate pricing models.

## Author
James Robinett (Jwallee)