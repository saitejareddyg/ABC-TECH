pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
        jdk 'JAVA_HOME'
    }
    environment {
        IMAGE_NAME = 'ABC-TECH'
        DOCKERHUB_USER = 'saiteja8270'
    }
    stages {
        stage('Checkout') { steps { git 'git@github.com:saitejareddyg/ABC-TECH.git' } }
        stage('Build') { steps { sh 'mvn clean compile' } }
        stage('Test') { steps { sh 'mvn test' } }
        stage('Package') { steps { sh 'mvn package -DskipTests' } }
        stage('Docker Build') { steps { sh 'docker build -t $DOCKERHUB_USER/$IMAGE_NAME .' } }
        stage('Docker Push') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKERHUB_PASS')]) {
                    sh '''
                    echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin
                    docker push $DOCKERHUB_USER/$IMAGE_NAME
                    '''
                }
            }
        }
    }
    post { always { cleanWs() } }
}
