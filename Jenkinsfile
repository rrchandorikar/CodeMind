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
        stage('Testing'){
            steps{
                sh 'echo Testing App version'
            }
        }
        stage('Create docker build'){
            steps{
                sh 'docker build -t cust_nginx:v4'
                sh 'sleep 5'
                sh 'docker tag cust_nginx:v4 codemindrohan/cust_nginx:v4'
                sh 'docker push codemindrohan/cust_nginx:v4'
            }
        }
    }
}
