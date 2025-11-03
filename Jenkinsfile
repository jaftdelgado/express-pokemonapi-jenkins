pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Clonando el repositorio..."
                git 'https://github.com/jaftdelgado/express-pokemonapi-jenkins.git'
            }
        }

        stage('Build') {
            steps {
                echo "Construyendo la imagen Docker..."
                bat 'docker build -t pokemon-api:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Desplegando la aplicación..."

                bat '''
                    docker stop pokemon-app-container || echo "No hay contenedor previo"
                    docker rm pokemon-app-container || echo "No hay contenedor previo"
                '''

                bat 'docker run -d --name pokemon-app-container -p 8081:3000 pokemon-api:latest'
            }
        }
    }

    post {
        always {
            echo "Pipeline terminado."
        }
    }
}
