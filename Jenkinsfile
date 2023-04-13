pipeline {
    agent any

    environment {
        google_cloud_composer_environment = 'airflow-from-jenkins'
        google_cloud_composer_location = 'us-central1'
        google_cloud_project_id = 'dark-axe-383408'
    }

    stages {
        stage('Trigger Google Cloud Composer') {
            steps {
                echo 'Activating Google Cloud Service Account and triggering Cloud Composer DAG...'
                withCredentials([file(credentialsId: 'dark-axe-383408', variable: 'google_cloud_key_file')]) {
                    sh '''gcloud auth activate-service-account --key-file="${google_cloud_key_file}"'''
                    sh '''gcloud config set project "${google_cloud_project_id}"'''
		    sh '''gcloud beta composer environments create "${google_cloud_composer_environment}" --location="${google_cloud_composer_location}" --image-version=composer-1.20.10-airflow-2.4.3 --machine-type=n1-standard-2 --node-count=3 --python-version=3 --project=my-project-id'''
                    sh '''gcloud composer environments run "${google_cloud_composer_environment}" --location="${google_cloud_composer_location}" trigger_dag -- 
--dag_id=automateML_Notification'''
                }
            }
        }
    }
}

