pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                // Checkout your repo
                git branch: 'main', url: 'https://github.com/Davina081004/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests; continue even if they fail
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                // Generate coverage report; continue even if it fails
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                // Run security audit; continue even if there are issues
                bat 'npm audit || exit /b 0'
            }
        }
    }
}

