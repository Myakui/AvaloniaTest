pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'  // Âåðñèÿ .NET SDK
        DOTNET_INSTALL_SCRIPT = 'dotnet-install.ps1'  // Óñòàíîâî÷íûé ñêðèïò äëÿ .NET
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Myakui/AvaloniaTest.git'
            }
        }
        stage('Restore dependencies') {
            steps {
                bat '$env:USERPROFILE\\.dotnet\\dotnet restore'
            }
        }
        stage('Build') {
            steps {
                bat '$env:USERPROFILE\\.dotnet\\dotnet build --configuration Release'
            }
        }
        stage('Test') {
            steps {
                bat '$env:USERPROFILE\\.dotnet\\dotnet test --configuration Release'
            }
        }
        stage('Publish') {
            steps {
                bat '$env:USERPROFILE\\.dotnet\\dotnet publish -c Release -o ./publish'
            }
        }
    }
}