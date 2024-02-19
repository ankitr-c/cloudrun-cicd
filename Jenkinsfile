pipeline {
    agent any

    parameters {
        string(name: 'REGION', defaultValue: 'us-central1', description: 'Region for Cloud Run service deployment')
        string(name: 'PORT', defaultValue: '8000', description: 'Port number for the deployed container')
        string(name: 'SERVICE_NAME', defaultValue: 'your-service-name', description: 'Name of the Cloud Run service')
        string(name: 'IMAGE', defaultValue: 'ankitraut0987/calc-app:1.0.0', description: 'Docker image to deploy to Cloud Run')
    }

    stages {
        stage('Authenticate') {
            steps {
                echo 'Inside Authentication'
                script {
                    withCredentials([file(credentialsId: 'cicd-key', variable: 'creds')]) {
                        sh "gcloud auth activate-service-account --key-file=${creds}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Inside Deploy'
                script {
                    sh "gcloud run deploy ${params.SERVICE_NAME} --image=${params.IMAGE} --platform=managed --region=${params.REGION} --port=${params.PORT} --allow-unauthenticated"
                }
            }
        }

        // stage('Allow allUsers') {
        //     steps {
        //         echo 'Inside Allow allUsers'
        //         script {
        //             sh'pwd'
        //         // sh "gcloud run services add-iam-policy-binding ${params.SERVICE_NAME} --region=${params.REGION} --member='allUsers' --role='roles/run.invoker'"
        //         }
        //     }
        // }
    }
}
