pipeline {
    agent {
        label any
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                expression { 
                    env.BRANCH_NAME == 'main' || env.BRANCH_NAME.startsWith('feature/')
                }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when {
                expression { 
                    env.BRANCH_NAME == 'develop' || env.BRANCH_NAME.startsWith('feature/')
                }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}