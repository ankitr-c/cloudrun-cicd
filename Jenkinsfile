pipeline {
    agent any
    environment {
                REGION = params.REGION
                PORT = params.PORT
                SERVICE_NAME = params.SERVICE_NAME
    }

    stages {
        stage('Authenticate') {
            steps {
                echo 'Inside Authentication'
                script {
                    withCredentials([file(credentialsId: 'cloudrun-cicd', variable: 'creds')]) {
                        sh "gcloud auth activate-service-account --key-file=${creds}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Inside Deploy'
                script {
                    sh "gcloud run deploy ${SERVICE_NAME} --image=ankitraut0987/calc-app:1.0.0 --platform=managed --region=${REGION} --port=${PORT}"
                }
            }
        }

        stage('Allow allUsers') {
            steps {
                echo 'Inside Allow allUsers'
                script {
                    sh "gcloud run services add-iam-policy-binding ${SERVICE_NAME} --region=${REGION} --member='allUsers' --role='roles/run.invoker'"
                }
            }
        }
    }
}
