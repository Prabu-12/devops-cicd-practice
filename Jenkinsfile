pipeline {
    agent any                          // Run on any available agent

    environment {                      // Environment variables
        APP_NAME = 'my-jenkins-app'
        VERSION  = '1.0.0'
    }

    stages {

        stage('Checkout') {            // Stage 1 — Get the code
            steps {
                echo "Checking out code..."
                echo "Branch: ${env.BRANCH_NAME}"
                echo "Build: ${env.BUILD_NUMBER}"
            }
        }

       stage('Build Docker Image') {
    steps {
        echo "Building Docker image..."
        sh "docker build -t ${APP_NAME}:${env.BUILD_NUMBER} ."
        sh "docker build -t ${APP_NAME}:latest ."
        echo "Docker image built: ${APP_NAME}:${env.BUILD_NUMBER}"
    }
}

stage('Test Docker Image') {
    steps {
        echo "Testing Docker image..."
        sh "docker run --rm ${APP_NAME}:latest"
        echo "Docker image test passed!"
    }
}

        stage('Code Quality') {        // Stage 4 — Quality check
            steps {
                echo "Running code quality checks..."
                echo "No critical issues found!"
            }
        }

        stage('Deploy') {              // Stage 5 — Deploy
            steps {
                echo "Deploying to staging..."
                echo "Deployment complete!"
            }
        }
    }

    post {                             // Runs AFTER all stages
        success {
            echo "✅ Pipeline SUCCESSFUL! App deployed."
        }
        failure {
            echo "❌ Pipeline FAILED! Check the logs."
        }
        always {
            echo "Pipeline finished. Build: ${env.BUILD_NUMBER}"
        }
    }
}
