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
                sh "gcloud auth activate-service-account jaivora@angelic-pipe-270921.iam.gserviceaccount.com --key-file=keyfile.json"
                sh "gcloud auth print-access-token | docker login -u oauth2accesstoken --password-stdin https://us.gcr.io"
                sh "gcloud auth configure-docker"
                sh "docker push gcr.io/angelic-pipe-270921/hello:${DOCKER_TAG}"
            }
        }
        stage('Deploy Image'){
            steps{
                sh "kubectl set image deployment/hello-web hello-app=gcr.io/angelic-pipe-270921/hello-app:${DOCKER_TAG}"
            }
        }
    }
}
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true;
    return tag
}
