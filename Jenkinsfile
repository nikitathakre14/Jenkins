pipeline {
    agent { label 'docker-node' } // Ensure builds run on your Jenkins agent

    environment {
        DOCKER_IMAGE = "nikita-devops-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
            }
        }

        stage('Merge Validation') {
            when {
                expression {
                    return env.BRANCH_NAME ==~ /feature\/.*/ || env.BRANCH_NAME == "main"
                }
            }
            steps {
                echo "Validating merge for branch: ${env.BRANCH_NAME}"
            }
        }
    }

    post {
        success {
            echo "Build succeeded for ${env.BRANCH_NAME}"
            // Optionally notify Jira or GitHub
        }
        failure {
            echo "Build failed for ${env.BRANCH_NAME}"
        }
    }
}

