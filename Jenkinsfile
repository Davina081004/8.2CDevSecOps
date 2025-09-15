pipeline {
    agent any

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
                bat 'npm test || exit 0'
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
                bat 'npm audit || exit 0'
            }
            post {
                always {
                    emailext(
                        to: 'davinaezra59@gmail.com',
                        subject: "Security Scan - Build,",
                        body: "",

                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit 0'
            }
        }
    }
}
