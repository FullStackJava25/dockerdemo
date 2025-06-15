pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/FullStackJava25/dockerdemo.git'
            }
        }

        stage('Build') {
            steps {
                bat '"%CD%\\mvnw.cmd" clean package'

            }
        }

        stage('Test') {
            steps {
                bat './mvnw test'
            }
        }

        stage('Deploy') {
            steps {
                bat 'java -jar target/*.jar'
            }
        }
    }
}
