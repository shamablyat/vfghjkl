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
                rm -rf vfghjkl
                git clone https://github.com/shamablyat/vfghjkl/--branch master
                cd vfghjkl 
                ls
                pwd
                docker compose up --build -d
                docker ps
                '''
            }
        }
        stage('build') {
            when {
                branch "main"
            }
            steps {
                sh '''
                rm -rf vfghjkl
                git clone https://github.com/shamablyat/vfghjkl/ --branch main
                cd vfghjkl 
                dotnet build
                whoami
                sshpass -f /root/pass scp -r root@47.76.135.185:/root/dotnet /var/lib/jenkins/workspace/dotnet_main/vfghjkl/bin/Debug/net6.0

                '''
            }
        }
        stage('deploy') {
            when {
                branch "main"
            }
            agent {
                label "slave1"
            }
            steps {
                sh '''
                sudo systemctl restart dotnet-jenkiins.service
                sudo systemctl status dotnet-jenkiins.service
                '''
            }
        }
    }
}