pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/aditya-sridhar/simple-reactjs-app.git'
            }
        }
        
        stage('Dependency Installation') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
              
                dir('src') {
                  
                    bat 'docker build -t scd .'
                }
            }
        }
        
        stage('Run Docker Image') {
            steps {
               bat 'docker run -d -p 8080:80 scd'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                   bat 'docker login -u $scd -p $kuro'
                   bat 'docker push scd'
                }
            }
        }
    }
}
