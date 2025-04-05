pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Myakui/AvaloniaTest.git'
            }
        }
        stage('Setup .NET') {
            steps {
                powershell 'Invoke-WebRequest https://dot.net/v1/dotnet-install.sh -OutFile dotnet-install.sh'
                powershell 'chmod +x dotnet-install.sh'
                powershell './dotnet-install.sh --version $env.DOTNET_VERSION'
                powershell '$env:PATH = "$HOME/.dotnet;$env:PATH"'
            }
        }
        stage('Restore dependencies') {
            steps {
                powershell '$HOME/.dotnet/dotnet restore'
            }
        }
        stage('Build') {
            steps {
                powershell '$HOME/.dotnet/dotnet build --configuration Release'
            }
        }
        stage('Test') {
            steps {
                powershell '$HOME/.dotnet/dotnet test --configuration Release'
            }
        }
        stage('Publish') {
            steps {
                powershell '$HOME/.dotnet/dotnet publish -c Release -o ./publish'
            }
        }
    }
}
