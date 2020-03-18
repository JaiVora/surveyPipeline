pipeline{
    agent any
        stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t gcr.io/angelic-pipe-270921/survey:latest"
            }
            
        }
        stage('Push Image'){
            steps{
                sh "gcloud auth activate-service-account jaivora@angelic-pipe-270921.iam.gserviceaccount.com --key-file=keyfile.json"
                sh "gcloud auth print-access-token | docker login -u oauth2accesstoken --password-stdin https://us.gcr.io"
                sh "gcloud auth configure-docker"
                sh "docker push gcr.io/angelic-pipe-270921/survey:latest"
            }
        }
    }
}

