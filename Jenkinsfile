pipeline {
    agent none
    stages {
        stage('jenkins_clone') {
            when {
                branch "main"
            }
            agent any
            steps {
                sh '''
                rm -rf repo
                git clone https://github.com/repo/ --branch main
                scp repo/path user@ip 
                rm -rf repo
                '''
            }
        }
    }
    stages {
        stage('docker') {
            when {
                branch "main"
            }
            agent application
            steps {
                sh '''
                cd repo/path
                docker images
                docker rmi image
                docker build -t tag .
                docker run image -p port
                docker ps
                '''
            }
        }
    }
}
