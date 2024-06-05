pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/KonduruBabu/Project-1.git/', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t KonduruBabu/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
        stage('Ddocker login'){
            steps{
                withCredentials([usernamePassword(CredentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')])
					sh "echo $PAS | docker login -u $USER -password-stdin"
                    sh 'docker push -t KonduruBabu/staragileprojectfinance:v1'
                    
					}
            }
        } 
        
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name Banking-container -p 8083:80 KonduruBabu/staragileprojectfinance:v1'
                  
                }
            }
        
    }

