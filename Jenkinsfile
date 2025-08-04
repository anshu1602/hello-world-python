pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anshu1602/hello-world-python.git'
                echo 'Code checkout completed'
            }
        }
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat "${scannerHome}\\bin\\sonar-scanner.bat"
                }
                echo 'SonarQube analysis completed'
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
                echo 'Quality gate check completed'
            }
        }
    }
}
