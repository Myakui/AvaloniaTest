pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'  // ������ .NET SDK
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/user/avalonia-project.git'
            }
        }
        stage('Setup .NET') {
            steps {
                sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                sh 'chmod +x dotnet-install.sh'
                sh './dotnet-install.sh --version $DOTNET_VERSION'
                sh 'export PATH=$HOME/.dotnet:$PATH'
            }
        }
        stage('Restore dependencies') {
            steps {
                sh '$HOME/.dotnet/dotnet restore'
            }
        }
        stage('Build') {
            steps {
                sh '$HOME/.dotnet/dotnet build --configuration Release'
            }
        }
        stage('Test') {
            steps {
                sh '$HOME/.dotnet/dotnet test --configuration Release'
            }
        }
        stage('Publish') {
            steps {
                sh '$HOME/.dotnet/dotnet publish -c Release -o ./publish'
            }
        }
    }
}
