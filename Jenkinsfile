pipeline {
    agent { label 'local-agent' }

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], description: 'Choisir l’environnement')
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
                changeset "**/*.py, Dockerfile"
            }
            steps {
                echo "Build Docker image..."
                sh 'docker build -t my-flask-app:latest .'
            }
        }
    }
}
