pipeline {
    agent any

    environment {
        IMAGE_NAME = "express-pokemons-api"
        IMAGE_TAG = "latest"
        DOCKERHUB_CREDENTIALS = 'dockerhub-credentials'
        DOCKERHUB_USER = 'tu-usuario'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Clonando el repositorio...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Construyendo la imagen Docker...'
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Desplegando el contenedor...'
                sh '''
                docker stop ${IMAGE_NAME} || true
                docker rm ${IMAGE_NAME} || true
                docker run -d -p 8080:3000 --name ${IMAGE_NAME} ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completado exitosamente!'
        }
        failure {
            echo 'Ocurrió un error. El pipeline falló.'
        }
    }
}
