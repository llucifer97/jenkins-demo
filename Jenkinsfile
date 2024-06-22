pipeline {
    agent any

    stages {
        stage('Hello World') {
            steps {
                echo 'Hello, World!'
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
