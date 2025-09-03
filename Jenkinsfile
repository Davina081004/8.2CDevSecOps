pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
        SNYK_TOKEN = credentials('synk-token')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Davina081004/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
        stage('Snyk Security Scan') {
            steps {
                // Set token and run Snyk test
                bat 'set SNYK_TOKEN=%SNYK_TOKEN% && snyk test'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                bat 'C:\\sonar-scanner\\bin\\sonar-scanner.bat -D"sonar.login=%SONAR_TOKEN%"'
            }
        }
    }
}
