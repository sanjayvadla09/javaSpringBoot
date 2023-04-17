pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                // Get some code from a GitHub repository
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Vamc1990/javaSpringBoot.git']])

            }
        }
        stage('Build') {
            steps {
                script {
                sh 'docker build -t "springapplication" .'

            }
            }    
            }
        stage('Checking the application status') {
            steps {
                script {
                    container_status = sh(script: "docker ps -a|grep -i springapplication", returnStatus: true) == 0
                    if ("${container_status}" ==  "true")
                    {
                    sh 'docker rm -f springapplication'
                    }
                }
        }
      }
            
        stage('Application start') {
            steps {
                script {
                sh 'docker run -d --name springapplication -p 8002:8080 springapplication'

            }
            }    
            }
            
        }
    }
        
  
