pipeline {
    agent any

    tools {
        nodejs 'NodeJS'  // Make sure this matches exactly
    }

    environment {
        CI = 'false' // React default, disable strict CI
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Vaibhavthanki/nextjs-vercel-app.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                withCredentials([string(credentialsId: 'vercel_test', variable: 'VERCEL_TOKEN')]) {
                    bat '''
                        npm install -g vercel
                        vercel --token=$VERCEL_TOKEN --prod --confirm
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ React app deployed to Vercel!"
        }
        failure {
            echo "❌ Deployment failed."
        }
    }
}