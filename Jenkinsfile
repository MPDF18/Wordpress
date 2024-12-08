pipeline {
    agent any

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
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') { // "SonarQube" debe coincidir con el nombre configurado en Jenkins
                        sh '''
                            mvn sonar:sonar \
                                -Dsonar.projectKey=myproject \
                                -Dsonar.host.url=${SONAR_HOST_URL} \
                                -Dsonar.sources=wp-content,wp-admin,wp-includes
                        '''
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

