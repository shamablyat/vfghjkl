pipeline {
    agent none
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
            agent any
            steps {
                sh '''
                rm -rf vfghjkl
                git clone https://github.com/shamablyat/vfghjkl/ --branch main
                cd vfghjkl 
                dotnet build
                scp -r /var/lib/jenkins/workspace/dotnet_main/vfghjkl/bin/Debug/net6.0/ root@47.76.135.185:/root/dotnet 
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
        stage('Get Commit Informaasdtion') {
            when {
                branch "main"
            }
            agent {
                label "slave1"
            }
            steps {
                script {
                    def commitInfo = sh(script: "git show -s --format='%an' ${env.GIT_COMMIT}", returnStdout: true).trim()
                    def commitMessage = sh(script: "git log -1 --pretty=%B ${env.GIT_COMMIT}", returnStdout: true).trim()
                    // echo "Commit author: ${commitInfo}"
                    sh "echo 'Commit author': '${commitInfo}'"
                    echo "Building ${env.BUILD_NUMBER} on ${env.NODE_NAME}"
                    echo "Commit Message: ${commitMessage}"
                    echo "Branch: ${env.GIT_BRANCH}"
                    def message = "Commit author: ${commitInfo} Building ${env.BUILD_NUMBER} on ${env.NODE_NAME} Commit Message: ${commitMessage} Branch: ${env.GIT_BRANCH}"
                    // sh "curl -X POST -H 'Content-Type: application/json' -d \"{'chat_id': '-4135540092', 'text': 'priv', 'disable_notification': false}\" 'https://api.telegram.org/bot6441756857:AAHVQhKc1IrnYo8UsZ-lqKRz9NnktcQww3Y/sendMessage'"
                    // def message = "Push event detected on branch: ${env.BRANCH_NAME}. Build successful!"
                    telegramSend message
                }
            }
        }
    }
}