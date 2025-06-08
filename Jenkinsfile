pipeline {
    agent { label 'linux-agent' }

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], description: 'Choisir l’environnement')
    }

    environment {
        APP_SECRET = credentials('APP_SECRET')
        API_TOKEN = credentials('API_TOKEN')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Build classique"
            }
        }

        stage('Build Image') {
            when {
                anyOf {
                    environment name: 'ENVIRONMENT', value: 'dev'
                    environment name: 'ENVIRONMENT', value: 'prod'
                }
            }
            steps {
                echo "🎯 Build de l'image avec Buildah"
                sh 'buildah bud -t my-flask-app:latest .'
            }
        }

        stage('Build Image Staging') {
            when {
                environment name: 'ENVIRONMENT', value: 'staging'
            }
            steps {
                echo "🎯 Build et tests spécifiques staging"
                sh 'buildah bud -t my-flask-app-staging:latest .'
            }
        }
    }
}
