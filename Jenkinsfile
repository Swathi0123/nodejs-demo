pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git credentialsId: '9f17d2c4-ef1a-4d1f-9ecd-10f6980d9e21', url: 'https://github.com/Swathi0123/nodejs-demo'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

