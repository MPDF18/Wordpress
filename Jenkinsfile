pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://192.168.11.134:9000' // Cambia la URL si es necesario
        SONAR_LOGIN = 'squ_6610f3699e1f57514eff796fb36c9068eeb191bb'  // Coloca tu token de SonarQube aquí
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MPDF18/Wordpress.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Realiza el análisis de SonarQube
                    withSonarQubeEnv('SonarQube') {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=myproject -Dsonar.sources=src'  // Ajusta los parámetros según sea necesario
                    }
                }
            }
        }
    }

    post {
        always {
            // Puedes agregar acciones post-build, como notificaciones o limpieza
            echo 'Pipeline finished'
        }
    }
}
