pipeline{
    agent any
    environment{
        DOCKER_TAG = getDockerTag()  
        PATH = "C:\\Program Files\\Git\\usr\\bin"
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build -t gcr.io/angelic-pipe-270921/hello:${DOCKER_TAG} ."
            }
            
        }
    }
}
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true;
    return tag
}