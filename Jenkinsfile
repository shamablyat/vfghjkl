pipeline {
    agent any
    stages {
        stage('docker') {
            when {
                branch "master"
            }
            steps {
                sh '''
                rm -rf test-dotnet
                git clone https://github.com/shamablyat/test-dotnet/
                cd test-dotnet 
                ls
                pwd
                docker compose up --build -d
                docker ps
                '''
            }
        }
        stage('dotnet') {
            when {
                branch "main"
            }
            steps {
                sh '''
                rm -rf test-dotnet
                git clone https://github.com/shamablyat/test-dotnet/
                cd test-dotnet 
                ls
                pwd
                dotnet run
                '''
            }
        }
    }
}