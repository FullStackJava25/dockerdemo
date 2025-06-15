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
                    def jarOutput = bat(script: 'dir /b target\\*.jar', returnStdout: true).trim()
                    if (jarOutput) {
                        def jarFile = jarOutput.split("\\r?\\n")[0]
                        echo "Deploying ${jarFile}"
                        bat "java -jar \"target\\${jarFile}\""
                    } else {
                        error "No JAR file found in target directory."
                    }
                }
            }
        }
    }
}
