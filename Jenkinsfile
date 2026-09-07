pipeline {
    agent any

    environment {
        IMAGE_NAME = 'aquarium'
        CONTAINER_NAME = 'aquarium'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build(IMAGE_NAME)
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    docker.image(IMAGE_NAME).run('-d -p 8080:80 --name ${CONTAINER_NAME}')
                }
            }
        }
    }

    post {
        always {
            sh "docker rm -f ${CONTAINER_NAME} || true"
        }
    }
}
