pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Ensure Yarn is Installed') {
            steps {
                // Check if yarn is installed; if not, install it using npm.
                sh '''
                    if ! command -v yarn > /dev/null 2>&1; then
                        echo "Yarn not found, installing Yarn..."
                        npm install -g yarn
                    else
                        echo "Yarn is already installed."
                    fi
                '''
            }
        }
        
        stage('Setup Environment File') {
            steps {
                // Write the .env file with your environment variables.
                sh '''
                    cat > .env <<EOF
                    HOST=0.0.0.0
                    PORT=1337
                    APP_KEYS="8d35c6e80f836ac1f3a2d47b,12c45f98e23a67b4d90m1p2n"
                    API_TOKEN_SALT=7f139dc8e54b2a36f890p4m2
                    ADMIN_JWT_SECRET=9c4e2b5a8f1d7h3j6k9m2n5p
                    TRANSFER_TOKEN_SALT=3b7n9p4m2k6h8j1d5f9g2s4
                    JWT_SECRET=5k8m2p7n4j1h6g9f3d5s8a2
                    EOF
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                // Use Yarn (or switch to npm if preferred)
                sh 'yarn install'
            }
        }
        
        stage('Build Admin Panel') {
            steps {
                echo 'Building the admin panel...'
                sh 'yarn build'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // For Strapi deployment you might want to use:
                sh 'yarn strapi deploy'
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
