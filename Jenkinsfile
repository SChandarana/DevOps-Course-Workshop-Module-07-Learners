pipeline {
    agent none
    environment {
        DOTNET_CLI_HOME = '/tmp/dotnet_cli_home'
    }
    stages {
        stage() {
            parallel {
                stage() {
                    agent {
                        docker {
                            image 'mcr.microsoft.com/dotnet/sdk:6.0'
                        }
                    }
                    stages {
                        stage('Build CSharp') {
                            steps {
                                sh 'dotnet build'
                            }
                        }
                        stage('Test CSharp') {
                            steps {
                                sh 'dotnet test'
                            }
                        }
                    }
                }
                stage() {
                    agent {
                        docker {
                            image 'node:17-bullseye'
                        }
                    }
                    stages {
                        stage('Build npm') {
                            steps {
                                dir('DotnetTemplate.Web') {
                                    sh 'npm install'
                                    sh 'npm run build'
                                }
                            }
                        }
                        stage('Run Linter') {
                            steps {
                                dir('DotnetTemplate.Web') {
                                    sh 'npm run lint'
                                }
                            }
                        }
                        stage('Run Typescript') {
                            steps {
                                dir('DotnetTemplate.Web') {
                                    sh 'npm t'
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
