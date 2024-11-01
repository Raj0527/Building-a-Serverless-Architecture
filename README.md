# Building-a-Serverless-Architecture

## Overview
As an **AWS Solutions Architect**, I have implemented a serverless, event-driven architecture using **Amazon Simple Notification Service (SNS)**, **Amazon Simple Queue Service (SQS)**, **AWS Lambda**, and **Amazon Simple Storage Service (S3)**. This setup demonstrates how to handle events in a strictly ordered manner, with message deduplication and filtering for specific processes. 

In this project, I configured an Amazon S3 bucket to trigger an SNS notification when an object is added. The SNS topic then distributes this notification to SQS queues, which in turn invoke AWS Lambda functions for processing the uploaded files. This architecture allows for decoupled, scalable processing without the need for server management.

The diagram below illustrates the complete workflow:

![Serverless](https://github.com/user-attachments/assets/ee4e0ccb-69ad-4e4e-a7f8-5fc95489f782)

## Objectives
Through this lab, I achieved the following:
- Set up SNS, SQS, and Lambda to create a decoupled, serverless event-driven architecture.
- Configured Amazon S3 to trigger notifications and invoke processes upon file uploads.
- Used AWS Lambda to automatically process files and log results to Amazon CloudWatch.

---

## Project Tasks
Each task below outlines the steps I followed to build the serverless environment on AWS.

### Task 1: Create a Standard Amazon SNS Topic
To set up notifications for file events:
1. I created an SNS topic that would act as the central notification system.
2. Subscribed to the SNS topic to allow downstream processing in other services.

### Task 2: Create Two Amazon SQS Queues
I set up SQS queues for specific processing needs:
- **Task 2.1:** Created an SQS queue for handling thumbnail image processing.
- **Task 2.2:** Created a separate SQS queue for mobile image processing.
3. Subscribed both SQS queues to the SNS topic to ensure they receive notifications when new files are uploaded to the S3 bucket.

### Task 3: Create an Amazon S3 Event Notification
To trigger events upon file uploads:
1. Configured an event notification on an Amazon S3 bucket that triggers SNS notifications when objects are added.
   - **Task 3.1:** Set the SNS topic access policy to allow the S3 bucket to publish messages.
   - **Task 3.2:** Created an S3 event notification that triggers on uploads to a designated S3 folder.

### Task 4: Create and Configure Two AWS Lambda Functions
For automated file processing, I set up two Lambda functions, each handling a specific image processing task.
- **Task 4.1:** Created a Lambda function named `CreateThumbnail`:
  - Configured an SQS trigger for this Lambda function to process messages from the SQS queue for thumbnail images.
  - Uploaded the function code for resizing images to thumbnail dimensions.
- **Task 4.2:** Uploaded a Python deployment package for `CreateThumbnail` and configured the SQS trigger.
- **Task 4.3:** Created another Lambda function for mobile image processing:
  - Added an SQS trigger to receive messages from the mobile image SQS queue.
  - Uploaded the code required for processing images for mobile compatibility.

### Task 5: Upload an Object to an Amazon S3 Bucket
To test the automated processing:
1. Uploaded a sample image to the designated folder in the S3 bucket.
   - **Task 5.1:** Used the S3 console to upload the image to the specified folder for processing, triggering the S3 event notification.

### Task 6: Validate the Processed File
After the upload, I validated that each Lambda function processed the image as expected:
- **Task 6.1:** Reviewed logs in Amazon CloudWatch Logs to verify that both Lambda functions processed the messages from SQS and resized the images.
- **Task 6.2:** Checked the S3 bucket folders for the processed thumbnail and mobile versions of the uploaded image.

---

## Conclusion
This serverless architecture demonstrates the power of decoupled, event-driven systems on AWS, providing scalability and reducing the need for infrastructure management. Each component in this project is designed to work together in a loosely coupled manner, making it easier to maintain and scale as needed.


## Author
This project was implemented as a hands-on lab to showcase my experience with AWS serverless and event-driven architecture. Through this exercise, I deepened my understanding of decoupling resources and automating workflows using AWS-managed services.
