pipeline{
    agent any
    environment{
        DOCKER_TAG = getDockerTag()  
        PATH = "C:\\Program Files\\Git\\usr\\bin;C:\\Program Files\\Git\\bin;${env.PATH}"
    }
    stages{
        stage('Build Docker Image'){
            steps{
                bat "sh -c docker build -t gcr.io/angelic-pipe-270921/hello:${DOCKER_TAG} ."
            }
            
        }
    }
}
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true;
    return tag
}