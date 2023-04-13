pipeline {
    agent any

    environment {
        google_cloud_key_file = 'project-owner-google-cloud-key-file'
        google_cloud_composer_environment = 'airflow-from-jenkins'
        google_cloud_composer_location = 'us-central1'
        google_cloud_project_id = 'dark-axe-383408'
    }

    stages {
        stage('Trigger Google Cloud Composer') {
            steps {
                echo 'Activating Google Cloud Service Account and triggering Cloud Composer 
DAG...'
                sh '''gcloud auth activate-service-account --key-file="${google_cloud_key_file}"
                gcloud config set project "${google_cloud_project_id}"
                gcloud composer environments run "${google_cloud_composer_environment}" --location="${google_cloud_composer_location}" trigger_dag -- --dag_id=automateML_Notification'''
            }
        }
    }
}

