pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore SampleApi.sln'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build SampleApi.sln --configuration Release --no-restore'
                sleep(time: 5, unit: 'SECONDS')
                echo 'Resuming after sleep'
            }
        }

        stage('Publish') {
            steps {
                bat 'dotnet publish SampleApi.csproj -c Release -o publish'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'publish/**', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build and artifact creation successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
