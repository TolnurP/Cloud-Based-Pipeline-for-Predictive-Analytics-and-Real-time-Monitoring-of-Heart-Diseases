# Cardio-Cloud: A Comprehensive Cloud-Based Pipeline for Predictive Analytics and Real-time Monitoring of Heart Diseases
## Overview
SuperZoom Manufacturing is dedicated to advancing heart health by utilizing cloud technology to provide real-time monitoring and predictive analytics for heart disease. Our system continuously collects health data, analyzes it using ML models in the cloud, and alerts users to potential heart risks, acting as a personal heart health assistant.

## Dataset
The dataset used for this project contains several attributes related to heart health, such as age, sex, blood pressure, cholesterol levels, and other medical conditions. The primary objective is to use these attributes to predict whether an individual is at risk of developing heart disease.

<b>Link to dataset :</b> https://www.kaggle.com/datasets/kamilpytlak/personal-key-indicators-of-heart-disease

## Files Description
•	Heart_Disease_Prediction_EDA.ipynb: 
This Jupyter notebook contains the exploratory data analysis (EDA) performed on the heart disease dataset. It includes data cleaning, visualization, and preliminary analysis.

•	heart-desease-prediction_data_preprocessing.ipynb: 
This notebook details the data preprocessing steps required to prepare the dataset for modeling, such as handling missing values, feature scaling, and data splitting.

•	heart-health-data.ipynb: 
This notebook provides an additional analysis of heart health data, focusing on different aspects not covered in the initial EDA.

•	heart-health-data_Modeling.ipynb: 
This notebook contains the modeling phase, where various machine learning algorithms are applied to predict heart disease. It includes model training, evaluation, and comparison.

•	personal_key_indicators_of_heart_disease.ipynb: 
This notebook explores personal key indicators of heart disease and how they correlate with the overall dataset findings.

## Installation
To run this project, you will need Jupyter Notebook or Jupyter Lab installed with Python 3.x. Additionally, the following Python packages are required: pandas, numpy, matplotlib, seaborn, scikit-learn. You can install these packages using pip

## Cloud Components
•	Amazon S3: Scalable object storage for organizing and storing data files.

•	AWS Kinesis: Real-time data streaming service for collecting and processing large volumes of data.

•	AWS Lambda: Serverless computing service for executing code in response to events, enabling efficient, event-driven applications.

•	Amazon SageMaker: Fully managed service that provides every developer and data scientist with the ability to build, train, and deploy machine learning (ML) models quickly.

•	Amazon API Gateway: Fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.

•	AWS Simple Notification Service (SNS): Pub/sub, SMS, email, and mobile push notifications service.

## Cloud Architecture:

![Cloud Architecture](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/Cloud%20Architecture.png)

## Implementation Workflow
### 1.	S3 Bucket: 
The S3 bucket consists of the dataset. The data set was directly uploaded from our local device to the S3 bucket. The data on the S3 bucket is used for training the Sagemaker model which predicts if a heart failure. The implementation on AWS is shown below.

![ S3 Bucket](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/S3%20Bucket.png) 

### 2.	AWS kinesis: 
The real-time data stream about the current heart condition is received from an IOT device. IOT devices like a smart watch, heart rate monitor or sensor can directly send the data to AWS kinesis. AWS Kinesis processes and transforms incoming data before forwarding it to the AWS SageMaker endpoint for predicting heart failure. We have created a kinesis instance on AWS as shown below.
 
![AWS kinesis](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/AWS%20Kinesis.png)

### 3.	AWS Sagemaker: 
The machine learning model to predict heart failure is trained on a sagemaker instance using a jupyter notebook. All machine learning tasks like cross validation, feature engineering, hyperparameter tuning were performed on the sagemaker instance. Random forest algorithm was found to be the best algorithm for the task at hand. 

![AWS Sagemaker](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/AWS%20Sagemaker.png)

### 4.	AWS Sagemaker Endpoint: 
The machine learning model, once trained, has been deployed as a SageMaker endpoint. This endpoint functions as a gateway for inferencing, allowing the model to process incoming data in real-time. A continuous stream of live data is directed to the endpoint from kinesis, facilitating continuous and real time inferencing to monitor and analyze the status of heart condition.

![AWS Sagemaker Endpoint](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/AWS%20Sagemaker%20Endpoint.png)

### 5.	REST API Integration: 
To enable inferencing from external devices, a Lambda function is utilized in conjunction with a REST API. This API is seamlessly connected to an external web application, providing a means for the SageMaker model to process incoming API calls for inferencing purposes.

### 6.	Lambda: 
An intricately designed Lambda function is established to actively oversee the predictions generated by the SageMaker endpoint. In the event that the SageMaker model predicts a "Yes" for heart failure, the Lambda function automatically initiates the AWS Simple Notification Service (SNS), ensuring timely and effective notifications are triggered.
 
![Lambda](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/Lambda.png)

### 7.	AWS Simple Notification Service (SNS): 
SNS will send a notification signaling the prediction of heart failure, prompting the opportunity for proactive preventive measures.

![AWS Simple Notification Service (SNS)](https://github.com/TolnurP/Cloud-Based-Pipeline-for-Predictive-Analytics-and-Real-time-Monitoring-of-Heart-Diseases/blob/main/Images/AWS%20Simple%20Notification%20Service%20(SNS).png)

## Cost Estimation
The monthly cost estimation for utilizing AWS resources is approximately $125.13, offering a scalable and cost-efficient solution for real-time heart health monitoring.

## Advantages and Disadvantages
•	Advantages: Scalability, cost efficiency, and seamless end-to-end integration.
•	Disadvantages: Potential delays due to increased volume, maintenance challenges, and cost management issues.

## Alternative Approaches
Initially considered AWS IoT Core and AWS CloudWatch for data ingestion and alerts, respectively, but were excluded due to use case specificity and simplicity/cost concerns.

