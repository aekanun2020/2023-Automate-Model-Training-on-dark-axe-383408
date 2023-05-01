# Project Title: Automate Model Training using DevOps

This project automates the process of model training using Jenkins, Google Cloud Composer (Airflow), and PySpark. The main 
file in this repository is a `Jenkinsfile`, which outlines the pipeline that checks out the Git repository, creates (or 
updates) a Google Cloud Composer environment, uploads Python and DAG files to Google Cloud Storage, and triggers the Cloud 
Composer environment to run the pipeline.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Pipeline Overview](#pipeline-overview)
- [Jenkinsfile Breakdown](#jenkinsfile-breakdown)
- [Included Files](#included-files)
- [Usage](#usage)

## Prerequisites

- Jenkins installation with the necessary plugins:
  - Git plugin
  - Credentials plugin
- Google Cloud SDK (gcloud) installed and configured on the Jenkins server
- Google Cloud Platform (GCP) project with appropriate permissions
- Google Cloud Composer environment (optional)

## Pipeline Overview

The Jenkins pipeline is comprised of the following stages:

1. Checkout Git repository
2. Trigger Google Cloud Composer

## Jenkinsfile Breakdown

The Jenkinsfile is a declarative pipeline that consists of the following sections:

1. **Environment Variables**: Set up the necessary environment variables required for the pipeline, such as GCP project ID, 
Cloud Composer environment and location, Git repo URL, branch, and PySpark bucket name.

2. **Stage 'Checkout Git repository'**: Clone the specified Git repository using the provided URL and branch.

3. **Stage 'Trigger Google Cloud Composer'**: Activate the GCP service account, check for the existence of the Cloud 
Composer environment, create it if not already present, upload Python and DAG files to GCS, and trigger the Cloud Composer 
environment to run the pipeline.

## Included Files

- `Jenkinsfile`: The main file containing the Jenkins pipeline definition
- `G-Student.py`: Python script for model training (upload to PySpark bucket)
- `refinedzone_H-Student.py`: Additional Python script for model training (upload to PySpark bucket)
- `DAG-automateML_Notification.py`: Airflow DAG file to orchestrate the pipeline (upload to Cloud Composer environment)

## Usage

1. Set up a Jenkins job to use the pipeline from this repository.
2. Configure the job's source code management to use your Git repository and the desired branch.
3. Create and configure the necessary credentials in Jenkins for your GCP service account key file.
4. Run the job to execute the pipeline, which will clone the Git repository, set up the Google Cloud Composer environment, 
and trigger the Airflow DAG to orchestrate the model training process.

Make sure to update the environment variables in the Jenkinsfile to match your GCP project, Cloud Composer environment, and 
other configurations as needed.

