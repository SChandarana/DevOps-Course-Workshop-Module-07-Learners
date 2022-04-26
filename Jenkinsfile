pipeline {
    agent none

    stages {
        stage('Build and test C#') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:6.0'
                }
            }
            steps {
                dotnet build
            }
        }
        stage('Build and test Typescript') {
            agent {
                docker {
                    image 'node:17-bullseye'
                }
            }
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
