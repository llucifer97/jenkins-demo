pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/llucifer97/jenkins-demo' // Replace with your GitHub repository URL
        MAVEN_HOME = tool 'M2_HOME' // Assumes Maven tool is configured in Jenkins
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
                    def mvnHome = tool name: 'M2_HOME', type: 'maven'
                    def mvnCmd = "${mvnHome}/bin/mvn" // Maven executable path
                    sh "${mvnCmd} clean package" // Execute Maven clean and package phases
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy and start the application, capturing output and errors
                script {
                    def deployCmd = "java -jar target/jenkins-ready.jar > app.log 2>&1 &"
                    sh deployCmd
                    // Print the deployment command output for debugging
                    sh 'tail -n 50 app.log' // Print last 50 lines of app.log for troubleshooting
                }
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
