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
  -Dsonar.projectKey=sonar1 \
  -Dsonar.projectName='sonar' \
  -Dsonar.host.url=http://192.168.11.134:9000 \
  -Dsonar.token=sqp_ebaa5ddef59a272c6b84fd048a70aef41c918121'
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

