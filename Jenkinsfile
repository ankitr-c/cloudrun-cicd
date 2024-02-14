pipeline {
    agent any
    stages {
        stage('Authenticate') {
            steps {
                sh '''
          gcloud auth activate-service-account --key-file="$GCLOUD_CREDS"
        '''
            }
        }
        stage('Install service') {
            steps {
                sh '''
          gcloud run services replace service.yaml --platform='managed' --region='us-central1'
        '''
            }
        }
        stage('Allow allUsers') {
            steps {
                sh '''
          gcloud run services add-iam-policy-binding hello --region='us-central1' --member='allUsers' --role='roles/run.invoker'
        '''
            }
        }
    }
}
