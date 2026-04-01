pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/subasinik-blip/simple-java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t my-java-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop my-app || true
                docker rm my-app || true
                docker run -d --name my-app my-java-app
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

    }
}
