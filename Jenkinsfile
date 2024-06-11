pipeline {
    agent any
    stages {
        stage('docker.') {
            when {
                branch "master"
            }
            steps {
                sh '''
                whoami
                '''
            }
        }
    }
}