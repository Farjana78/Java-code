pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven-3.8.7'
        DEPLOY_USER = 'deploy'
        DEPLOY_PASS = 'deploy123'
        TOMCAT_URL = 'http://65.2.132.47:8080/manager/text'
        APP_NAME = 'myapp'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Farjana78/Java-code.git'
            }
        }

        stage('Build') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean package"
            }
        }

        stage('Deploy') {
            steps {
                deploy adapters: [tomcat10(
                    credentialsId: 'tomcat-credentials',
                    path: '',
                    url: "${TOMCAT_URL}"
                )], contextPath: "${APP_NAME}", war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
