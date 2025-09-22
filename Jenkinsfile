pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Nikithpb/Devops.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'zip -r build.zip . -x "*.git*" -x "node_modules/*"'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build.zip', fingerprint: true
            }
        }

        stage('Notify') {
            steps {
                echo "Build finished for ${env.JOB_NAME} #${env.BUILD_NUMBER}"
            }
        }
    }

    post {
        success { echo 'SUCCESS' }
        failure { echo 'FAILURE' }
    }
}

