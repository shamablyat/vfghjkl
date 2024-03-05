pipeline {
    agent {
        label "slave1"
       }
    stages {
        stage('docker') {
            when {
                branch "master"
            }
            steps {
                sh '''
                rm -rf test-dotnet
                git clone https://github.com/shamablyat/vfghjkl/--branch master
                cd vfghjkl 
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
                git clone https://github.com/shamablyat/vfghjkl/ --branch main
                cd vfghjkl 
                dotnet build
                sudo systemctl restart dotnet-test.service
                sudo systemctl status dotnet-test.service
                '''
            }
        }
    }
}