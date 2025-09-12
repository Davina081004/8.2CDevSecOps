pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your_github_username/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
            post {
                always {
                    emailext(
                        to: 'davinawong1008@gmail.com',
                        subject: "Test Stage - Build ${currentBuild.currentResult}",
                        body: """\
Hello,

The **Test** stage for build ${env.BUILD_NUMBER} has completed.
Build Status: ${currentBuild.currentResult}

Attached are the logs for this stage.

Thanks,
Jenkins
""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    emailext(
                        to: 'davinawong1008@gmail.com',
                        subject: "Security Scan - Build ${currentBuild.currentResult}",
                        body: """\
Hello,

The **Security Scan** stage for build ${env.BUILD_NUMBER} has completed.
Build Status: ${currentBuild.currentResult}

Attached are the logs for this stage.

Thanks,
Jenkins
""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
    }
}

