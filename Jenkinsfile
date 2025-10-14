pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven'
        DEPLOY_USER = 'deploy'
        DEPLOY_PASS = 'deploy123'
        TOMCAT_URL = 'http://<server-ip>:8080/manager/text'
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
                deploy adapters: [tomcat9(
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
