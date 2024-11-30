pipeline {
    agent any
    tools {
        // Use the .NET SDK tool name as configured in Jenkins
        dotnetsdk 'NET' 
    }
    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/FrancescoPaoloL/CSharp4JenkinsTestsExample.git'
            }
        }
        stage('Restore Dependencies') {
            steps {
                echo 'Restoring dependencies...'
                sh 'dotnet restore'
            }
        }
        stage('Build Project') {
            steps {
                echo 'Building the project...'
                sh 'dotnet build --configuration Release'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'dotnet test --configuration Release'
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
