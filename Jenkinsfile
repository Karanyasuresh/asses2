pipeline {
    agent any

    tools {
        nodejs 'nodejs-22.12.0'  // Use the Node.js tool defined in Jenkins
    }

    environment {
        SONAR_SCANNER_PATH = 'C:/Users/karan/Downloads/sonar-scanner-cli-6.2.1.4610-windows-x64/sonar-scanner-6.2.1.4610-windows-x64/bin'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm  // Check out the latest code from your version control system
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                npm install
                '''
            }
        }

        stage('Lint') {
            steps {
                bat '''
                npm run lint -- --fix
                '''
            }
        }

        stage('Build') {
            steps {
                bat '''
                npm run build
                '''
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonar-token')  // Retrieve SonarQube token from Jenkins credentials
            }
            steps {
                bat '''
                set PATH=%SONAR_SCANNER_PATH%;%PATH%
                where sonar-scanner || echo "SonarQube scanner not found. Please install it."
                sonar-scanner -Dsonar.projectKey=asses2 ^ 
                              -Dsonar.sources=. ^ 
                              -Dsonar.host.url=http://localhost:9000 ^ 
                              -Dsonar.token=%SONAR_TOKEN%
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
        always {
            echo 'This runs regardless of the result.'
        }
    }
}
