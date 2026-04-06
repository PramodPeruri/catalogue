pipeline {
    agent {
        node{
            label 'AGENT-1'
        }
    }
    environment {
        COURSE= "Jenkins"
        appVersion = ""
        ACC_ID = "791272971151"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
    }
    stages {
        stage('Read Version') {
            steps {
                script{
                   def packageJSON = readJSON file: 'package.json'
                   appVersion = packageJSON.version
                   echo "app version: ${appVersion}"
                }
                
            }
        }
        stage('Install Dependencies') {
            steps {
                script{
                   sh """
                       npm install
                   """
                }
            }
        }
        stage('Unit Test') {
            steps {
                script{
                   sh """
                       npm test
                   """
                }
            }
        }
        stage('Build Image') {
            steps {
                script{
                   withAWS(region:'us-east-1',credentials:'aws-creds') {
                                sh """
                                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                                  docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .
                                  docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                                   """

                               }

                }
            }
        }
        
    }
    post {
         always {
            cleanWs() // Deletes the entire workspace
          }
         success {
                echo 'I will run if success'
         }
         failure{
               echo 'I will run if failure'
         }

        }
}