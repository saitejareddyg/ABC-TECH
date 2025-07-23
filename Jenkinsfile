pipeline {
    agent any

    environment {
        IMAGE_NAME = "saiteja/abc-tech"
        IMAGE_TAG  = "v1"
    }

    stages {
        stage('Clone') {
            steps {
                git 'git@github.com:saitejareddyg/ABC-TECH.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build & Push') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }

    post {
        always {
            echo 'Build and Docker push complete.'
        }
    }
}
