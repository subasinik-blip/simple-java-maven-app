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
        script {
            docker.build('my-java-app', '.')
        }
    }
}

        stage('Deploy') {
    steps {
        script {
            def exists = sh(script: "docker ps -a -q -f name=my-app", returnStdout: true).trim()
            if (exists) {
                sh "docker stop my-app"
                sh "docker rm my-app"
            }
            sh "docker run -d --name my-app -p 8080:8080 my-java-app"
        }
    }
}

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

    }
}
