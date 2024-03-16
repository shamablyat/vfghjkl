pipeline {
    agent any
    stages {
        stage('docker') {
            when {
                branch "main"
            }
            steps {
                sh '''
                cd /home/e-moliya
                rm -rf uzasbo2_backend
                git clone https://github.com/webaseuz/uzasbo2_backend --branch main-xtmbat
                pwd
                // scp /path user@ip 
                // rm -rf repo
                // cd repo/path
                // docker images
                // docker rmi image
                // docker build -t tag .
                // docker run image -p port
                // docker ps
                '''
            }
        }
    }
}
