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
               bat '''
               call mvnw.cmd clean package
               '''
           }
       }

       stage('Test') {
           steps {
               bat '''
               call mvnw.cmd test
               '''
           }
       }

        stage('Deploy') {
            steps {
                script {
                    def jarFiles = bat(script: 'dir /b target\\*.jar', returnStdout: true).trim().split("\r\n")
                    if (jarFiles.length > 0) {
                        bat "java -jar \"target\\${jarFiles[0]}\""
                    } else {
                        error "No JAR file found in target directory."
                    }
                }
            }
        }
    }
}
