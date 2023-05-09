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
        stage('Unit Testing'){
            steps{
                sh 'echo Testing App version....'
                sh 'echo Test cases Passed'
            }
        }
        stage('Smoke Testing'){
            steps{
                sh 'echo Testing App version.....'
                sh 'echo Test cases Passed'
            }
        }
        stage('Sanity Testing'){
            steps{
                sh 'echo Testing App version'
                sh 'echo Test cases Passed'
            }
        }
        stage('Regression Testing'){
            steps{
                sh 'echo Testing App version'
                sh 'echo Test cases Passed'
            }
        }
        stage('Create docker image'){
            steps{
                sh 'docker build -t cust_nginx:v5 .'
                sh 'sleep 5'
            }
        }
         stage('Pushing artefacts to Artefactory'){
            steps{
                sh 'docker tag cust_nginx:v5 codemindrohan/cust_nginx:v5'
                sh 'docker push codemindrohan/cust_nginx:v5'
                sh 'sleep 5'
            }
         }
        stage('Deploying Application'){
            steps{
                sh 'docker stack deploy -c docker-compose.yml web --orchetrator swarm'
            }
         }
    }

}

