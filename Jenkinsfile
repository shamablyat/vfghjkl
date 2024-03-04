pipeline {
    agent any
    stages {
        stage('docker.') {
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
        stage('dotnet.') {
            when {
                branch "main"
            }
            steps {
                sh '''
                rm -rf test-dotnet
                git clone https://github.com/shamablyat/test-dotnet/ --branch main
                cd test-dotnet 
                dotnet build
                sudo systemctl restart dotnet-test.service
                sudo systemctl status dotnet-test.service
                '''
            }
        }
    }
}