pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the project'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded'
        }
    }
}

