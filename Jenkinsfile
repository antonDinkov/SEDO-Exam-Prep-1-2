pipeline {
    agent { label 'windows' }

    triggers {
        // Ако Jenkins е Multibranch pipeline, не е нужно.
        // pollSCM('H/5 * * * *') // опционално – проверява repo-то на всеки 5 минути
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup .NET 6') {
            steps {
                bat 'dotnet --version'
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
                    env.BRANCH_NAME == 'develop' || env.BRANCH_NAME.startsWith('feature/')
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

    post {
        always {
            junit '**/TestResults/*.xml' // ако се генерират JUnit-compatible резултати
            cleanWs() // изчиства workspace-а след билда
        }
    }
}