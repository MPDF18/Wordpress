pipeline {
    agent any
    environment {
	PATH = "$PATH:/usr/share/maven"	
    }

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio desde GitHub
                git 'https://github.com/MPDF18/Wordpress.git'
            }
        }

        stage('Build') {
            steps {
                // Construir el proyecto con Maven
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('sonar-v24.12.0') { // "SonarQube" debe coincidir con el nombre configurado en Jenkins
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
    }

    post {
        always {
            // Limpieza o notificaciones al finalizar el pipeline
            echo 'Pipeline finished'
        }
    }
}

