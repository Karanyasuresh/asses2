
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Check out code from GitHub repository
                git branch: 'main', url: 'https://github.com/your-repository-url.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install dependencies using npm
                script {
                    sh 'npm install'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
