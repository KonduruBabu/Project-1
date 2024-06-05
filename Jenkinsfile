pipeline {
    agent any
    stages {
        stage('Build Project') {
            steps {
                git url: 'https://github.com/KonduruBabu/Project-1.git', branch: 'master'
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t kondurubabu/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'echo "$PASS" | docker login -u "$USER" --password-stdin'
                    sh 'docker push kondurubabu/staragileprojectfinance:v1'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name Banking-container -p 8083:80 kondurubabu/staragileprojectfinance:v1'
            }
        }
    }
}
