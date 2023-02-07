pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
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
                    app = docker.build("underwater")
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
                        docker.withRegistry('https://288694353266.dkr.ecr.us-east-1.amazonaws.com/jenkins-test', 'ecr:ecr.us-east-1:AKIAUGN4GHVZKMXT7DGP,ePCz8Hg5aX7Sp7T7fIdGI7IoEFlCzDGhfewEdTgV') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}
