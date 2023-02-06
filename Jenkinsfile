pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    
    environment {
        registry = "288694353266.dkr.ecr.us-east-1.amazonaws.com/jenkins-test"
    }
    
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        
        stage('Build') { 
            steps { 
                script{
                 dockerImage = docker.build registry
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('https://288694353266.dkr.ecr.us-east-1.amazonaws.com/jenkins-test', 'ecr:ecr.us-east-1:<Your Jenkins Credentials>') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}
