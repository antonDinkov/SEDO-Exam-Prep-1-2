pipeline {
    agent any

    stages {
        stage('Checkout') {
            when {
                anyof {
                    branch 'develop'
                    branch 'main'
                }
            }
            steps {
                checkout scm
            }
        }

        stage('Restore dependencies') {
            when {
                anyof {
                    branch 'develop'
                    branch 'main'
                }
            }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                anyof {
                    branch 'develop'
                    branch 'main'
                }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when {
                anyof {
                    branch 'develop'
                    branch 'main'
                }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}