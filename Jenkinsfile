pipeline {
    agent any

    environment {
        google_cloud_composer_environment = 'airflow-from-jenkins'
        google_cloud_composer_location = 'us-central1'
        google_cloud_project_id = 'dark-axe-383408'
	google_cloud_composer_environment_api_version = 'v1' // ระบุเวอร์ชัน API เป็น v1
    }

    stages {
        stage('Trigger Google Cloud Composer') {
            steps {
                echo 'Activating Google Cloud Service Account and triggering Cloud Composer DAG...'
                withCredentials([file(credentialsId: 'dark-axe-383408', variable: 'google_cloud_key_file')]) {
                    sh '''gcloud auth activate-service-account --key-file="${google_cloud_key_file}"'''
                    sh '''gcloud config set project "${google_cloud_project_id}"'''
		    sh '''gcloud beta composer environments create "${google_cloud_composer_environment}" --location="${google_cloud_composer_location}" --api-version="${google_cloud_composer_environment_api_version}"''' // ระบุเวอร์ชัน API เป็น v1
                    sh '''gcloud composer environments run "${google_cloud_composer_environment}" --location="${google_cloud_composer_location}" trigger_dag -- 
--dag_id=automateML_Notification'''
                }
            }
        }
    }
}

