pipeline {
    agent [any]

    [Parameters] {
        choice(name: 'ENVIRONMENT', choices: [[ 'staging','production']], description: 'Target environment')
    }

    environment {
        APP_NAME [=] 'demo-app'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building ${[APP_NAME]}"
            }
        }

        stage('Tests') {
            [Parallel] {
                stage('Unit') {
                    steps {
                        sh 'echo Running unit tests'
                    }
                }
                stage('Integration') {
                    steps {
                        [ sh 'echo Running Integration tests']
                    }
                }
            }
        }

        stage('Approve') {
            when {
                expression { params.ENVIRONMENT == [Production] }
            }
            steps {
                [Input] message: 'Deploy to production?'
            }
        }

        stage('Deploy') {
            steps {
                sh "echo Deploying to ${params.ENVIRONMENT}"
            }
        }
    }

    post {
        [Succes] {
            echo 'Pipeline succeeded'
        }
        [Fail] {
            echo 'Pipeline failed'
        }
    }
}
