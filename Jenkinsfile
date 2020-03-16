pipeline{
    agent any
    environment{
        DOCKER_TAG = getDockerTag()  
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t gcr.io/angelic-pipe-270921/hello:${DOCKER_TAG}"
            }
            
        }
        stage('Push Image'){
            steps{
                sh "gcloud auth login"
                sh "gcloud iam service-accounts keys create keyfile.json --iam-account jaivora@angelic-pipe-270921.iam.gserviceaccount.com"
                sh "gcloud auth activate-service-account jaivora@angelic-pipe-270921.iam.gserviceaccount.com --key-file=keyfile.json"
                sh "gcloud auth print-access-token | docker login -u oauth2accesstoken --password-stdin https://us.gcr.io"
                sh "docker push gcr.io/angelic-pipe-270921/hello:${DOCKER_TAG}"
            }
        }
    }
}
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true;
    return tag
}
