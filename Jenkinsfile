pipeline {
    agent {
        node{
            label 'AGENT-1'
        }
    }
    environment {
        COURSE= "Jenkins"
        appVersion = ""
    }
    stages {
        stage('Read Version') {
            steps {
                script{
                   def packageJSON = readJSON file: 'db/package.json'
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
        // stage('Build Image') {
        //     steps {
        //         script{
        //            sh """
        //                docker build -t catalogue:${appVersion}
        //            """
        //         }
        //     }
        // }
        stage('Deploy') {
            // input {
            //     message "Should we continue?"
            //     ok "Yes, we should."
            //     submitter "alice,bob"
            //     parameters {
            //         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
            //     }
            // }
            steps {
                script{
                   sh """
                       echo "Deploying."
                   """
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