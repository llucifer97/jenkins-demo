pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/llucifer97/jenkins-demo' // Replace with your GitHub repository URL
        M2_HOME = '/Applications/apache-maven-3.9.6'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: "${GIT_REPO}"]]])
            }
        }

        stage('Build') {
            steps {
                script {
                    def mvnHome = tool name: 'Maven', type: 'maven'
                    def mvnCmd = "${mvnHome}/bin/mvn" // Maven executable path
                    sh "${mvnCmd} clean package" // Execute Maven clean and package phases
                }
            }
        }

        stage('Deploy') {
            steps {
                sh "java -jar target/jenkins-ready.jar &" // Example deployment command
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
