# Early detection of Diabetes
<p align="center">
  <img width="900" height="600" src="https://www.cdc.gov/diabetes/images/library/spotlights/diabetes-stats-report-724px.png?_=42420">
</p>
 
## 1.0 Objective
- Create a machine learning model to detect diabetes early
- Build, train as well as deploy the model on AWS Sagemaker
<p align="center">
  <img width="250" height="200" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS5VU4gGNe1QWsmHdcrAWuUVvcK49yqZU_HAWJLKCR4dDUlmH_SY9EXs9g50FJ16NuCFNM&usqp=CAU">
</p>

## 2.0 Steps to Build, Train and Deploy Machine Learning Models in AWS Sagemaker
- Following are the steps required to work on a ML model in AWS Sagemaker after creating an AWS Account:
  - Create new Amazon Sagemaker Notebook Instance
  - Create new S3 Bucket
  - Create ML Classifier instance
  - Train the model
  - Deploy the model on Sagemaker
  - Evaluation
  
 ### 2.1 Amazon Sagemaker Notebook Instance
- This is the step wherein we create a new python3 jupyter notebook.
- We also create an Identity and Access Management (IAM) role that allows Amazon SageMaker to access data in Amazon Simple Storage Service (Amazon S3).
- Following are steps mentioned on the AWS "Getting Started" page:
    - On the Create notebook instance page, in the Notebook instance setting box, fill the following fields:
      - For Notebook instance name, type diabetes_detection.
      - For Notebook instance type, choose ml.t2.medium.
      - For Elastic inference, keep the default selection of none.
      - For Platform identifier, keep the default selection.
    - In the Permissions and encryption section, for IAM role, choose Create a new role, and in the Create an IAM role dialog box, select Any S3 bucket and choose Create role. Refer below image for the same:
  ![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/01%20instance%20creation.JPG)
    - Keep the default settings for the remaining options and choose Create notebook instance.
- In the Notebook instances section, the new SageMaker-Tutorial notebook instance is displayed with a Status of Pending. The notebook is ready when the Status changes to InService. Below image shows the same: 
 ![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/02%20instance%20status.JPG)
 
### 2.2 S3 Bucket
- Using boto3, create a new S3 bucket named diabetes-detection-bucket.
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/03%20S3%20Bucket.JPG)
- This is the place where all the train, test data is stored after splitting the dataset.
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/04%20Folders%20inside%20S3%20bucket.JPG)
- The train data should have the predictor variable as the first column and the independent variables succeeding it.

### 2.3 XGB Classifier Instance
- XGB Classifier is used for the current project in order to predict whether the patient has diabetes or not.
- Set up the Amazon SageMaker session, create an instance of the XGBoost model (an estimator), and define the model’s hyperparameters.


### 2.4 Train the model
- Using xgb.fit, we start the training of the model.
- The training jobs contains information about the Algorithm, its hyperparameters, timestamp of creation, Failure Reason if any, etc.
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/05%20model%20training%20in%20progress.JPG)

### 2.5 Deployment
- xgb.deploy saves the model within the Sagemaker models which can be called for predictions
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/07%20model.JPG)
- End points are created as well to provide realtime inference if required.
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/08%20endpoints.JPG)

### 2.6 Evaluation
- Once the model is deployed, the same can be called for predicting on test data and evaluating the performance.
- To analyze data and evaluate machine learning models on Amazon SageMaker, Processing jobs can also be utilised.
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/06%20processing%20jobs.JPG)
- With Processing, we can use a simplified, managed experience on SageMaker to run data processing workloads, such as feature engineering, data validation, model evaluation, and model interpretation. 
- We can also use the Amazon SageMaker Processing APIs during the experimentation phase and after the code is deployed in production to evaluate performance.

### 2.7 Final Steps
- In this step, we terminate the resources used.
- Terminating resources that are not actively being used reduces costs and is a best practice. 
- Not terminating resources will result in charges to your account.
- The model endpoints needs to be deleted as well as all the resources by using boto3 within the notebook.
- Stop and Delete the notebook if the same is not required as well.
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/09%20stopping%20notebook.JPG)
![](https://github.com/sanjayd89/Diabetes_detection_on_AWS_Sagemaker/blob/main/images/10%20deleting%20notebook.JPG)
