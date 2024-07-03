pipeline {
    agent {
        label 'your-agent-label' // Replace with your agent's label
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
                script {
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}:latest").push()
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
