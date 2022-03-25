 String branchName = "newone"
 String gitCredentials = "6c6c44c2-0f07-40bd-b4a5-238abd94a39a"
 String repoUrl = "https://github.com/sagarkivale101/aws.git"

pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
             //   checkout scm
                git branch: branchName, credentialsId: 	gitCredentials, url: repoUrl
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("samk101/dockerdemo")
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
                  // /samk101/dockerdemo
                  //   docker.withRegistry('https://720766170633.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:aws-credentials') {
                     docker.withRegistry('https://712997808987.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-credentials') {
                    
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}

