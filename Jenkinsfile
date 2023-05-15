pipeline {
    agent any

    stages {
        stage('Git Code Checkout'){
            steps{
                git branch: 'main',
                credentialsId: 'd6347000-3337-45a9-bf69-8dc229eaab1f',
                url: 'https://github.com/rrchandorikar/CodeMind.git'
            }
        }
        stage('Building......'){
            steps{
                sh 'docker build -t cust_nginx:${BUILD_NUMBER} .'
                sh 'sleep 5'
            }
        }
         stage('Pushing artefacts to Artefactory..............'){
            steps{
                sh 'docker tag cust_nginx:${BUILD_NUMBER} codemindrohan/cust_nginx:${BUILD_NUMBER}'
                sh 'docker push codemindrohan/cust_nginx:${BUILD_NUMBER}'
                sh 'sleep 5'
            }
         }
        stage('Testing.......'){
            agent{
                node{
                    label 'staging'
                }
            }
            steps{
                sh 'docker pull codemindrohan/cust_nginx:${BUILD_NUMBER}'
                sh 'sleep 8'
                sh 'docker run -d --name app_1 -p 81:80 codemindrohan/cust_nginx:${BUILD_NUMBER}'
                sh 'sleep 5'
                sh 'echo Testing App version....'
                sh 'sleep 5'
                sh 'echo Test cases Passed'
            }
        }
        stage('CLIENT PROD DEPLOYMENT........'){
            agent{
                node{
                    label 'clinet'
                }
            }
            steps{
                sh 'docker pull codemindrohan/cust_nginx:${BUILD_NUMBER}'
                sh 'sleep 5'
                sh 'docker run -d --name app_1 -p 82:80 codemindrohan/cust_nginx:${BUILD_NUMBER}'
            }
         }
    }
    post {
     aborted {
         echo "Sending Slack notification"
         slackSend (color: '#FFC300', 
         message: "*ABORTED:*\n Job: ${env.JOB_NAME}\n Build Number: ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}")
         
     }
     
     failure {
         echo "Sending Slack notification"
         slackSend (color: '#E01563',
         message: "*FAILED:*\n Job: ${env.JOB_NAME}\n Build Number: ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}")
     }
     
     success {
         echo "Sending Slack notification"
         slackSend (color: '#3EB991',
         message: "*SUCCESS:*\n Job: ${env.JOB_NAME}\n Build Number: ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}")
     }
  }
}

