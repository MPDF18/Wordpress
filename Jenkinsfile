pipeline {
    agent any
    environment {
	PATH = "$PATH:/usr/share/maven"	
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MPDF18/Wordpress.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('sonar-v24.12.0') {
                        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=sonar-1 \
  -Dsonar.projectName='sonar-1' \
  -Dsonar.host.url=http://192.168.11.134:9000 \
  -Dsonar.token=sqp_5afc4ea1120a1c9c1e1734f2612326edd89781fa'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}

