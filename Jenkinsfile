pipeline {
    agent any

    environment {
        NODE_ENV = 'production' // Set Node environment
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install' // Or 'yarn install' if you're using Yarn
            }
        }
        
        stage('Build Admin Panel') {
            steps {
                echo 'Building the admin panel...'
                sh 'npm run build' // Or 'yarn build' if you're using Yarn
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test' // Or 'yarn test' if your project has tests
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'npm run start' // Or 'yarn start' for deployment
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
