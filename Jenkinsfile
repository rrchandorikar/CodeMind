pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'mkdir pipelinetest'
                sh 'cp pipelinetest /home/ubuntu/CICD/'
            }
        }
        stage('Git Code Checkout'){
            steps{
                git branch: 'main',
                credentialsId: 'd6347000-3337-45a9-bf69-8dc229eaab1f',
                url: 'https://github.com/rrchandorikar/CodeMind.git'
            }
        }
    }
}
