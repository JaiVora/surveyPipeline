pipeline{
    agent any
    environment{
        DOCKER_TAG = getDockerTag()  
    }
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
                sh "docker push gcr.io/angelic-pipe-270921/survey:v1"
            }
        }
        stage('Deploy Image'){
            steps{
                sh "gcloud auth activate-service-account jaivora@angelic-pipe-270921.iam.gserviceaccount.com --key-file=keyfile.json"
                sh "gcloud auth print-access-token | docker login -u oauth2accesstoken --password-stdin https://us.gcr.io"
                sh "gcloud auth configure-docker"
                sh "gcloud container clusters get-credentials hello-cluster --region us-east4 --project angelic-pipe-270921"
                sh "/home/jai/Downloads/google-cloud-sdk/bin/kubectl delete --all pods"
                sh "/home/jai/Downloads/google-cloud-sdk/bin/kubectl set image deployment/hello-web survey=gcr.io/angelic-pipe-270921/survey:v1"
            }
        }
    }
}
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true;
    return tag
}
