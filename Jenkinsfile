pipeline {
    agent {
        label 'dev' // Replace with your agent's label
    }

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-78' 
        DOCKER_IMAGE = 'yakametehan/jenkins-pipeline-practice' 
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mete20/jenkins-pipeline-practice.git' 
            }
        }

        stage('Build') {
            steps {
                sh 'sudo docker build -t ${DOCKER_IMAGE}:latest .'
            }
        }

        stage('Push') {
            steps {
                script {
                    withCredentials([string(credentialsId: "${DOCKER_CREDENTIALS_ID}", variable: 'DOCKERHUB_CREDENTIALS')]) {
                        sh 'echo ${DOCKERHUB_CREDENTIALS} | docker login -u yakametehan --password-stdin'
                        sh 'sudo docker push ${DOCKER_IMAGE}:latest'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
