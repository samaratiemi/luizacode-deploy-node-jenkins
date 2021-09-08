pipeline {
    agent any
    tools { nodejs "node" }
    environment {
        DOCKERHUB_CRED = credentials('dockerhub-token')
    }
    stages {
        stage('Build') {
            steps {
                sh """
                    docker build -t luizacode-deploy-node-jenkins:latest .
                """
            }
        stage('Test') {
            steps {
                sh 'npm install'
                sh """
                    npm test
                """
        }
        stage('Publish') {
            steps {
                sh 'echo $DOCKERHUB_CRED_PSW | docker login -u $DOCKERHUB_CRED_USR --password-stdin'
                sh """
                   docker push $DOCKERHUB_CRED_USR/luizacode-deploy-node-jenkins:latest
                """
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }

}