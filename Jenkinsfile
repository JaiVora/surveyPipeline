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
                sh ""docker login -u vora.jai1@gmail.com -p chintan28058562 gcr.io"
                sh "docker push gcr.io/angelic-pipe-270921/hello:${DOCKER_TAG}"
            }
        }
    }
}
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true;
    return tag
}
