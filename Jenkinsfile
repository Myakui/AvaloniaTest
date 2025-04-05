pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'  // Версия .NET SDK
        DOTNET_INSTALL_SCRIPT = 'dotnet-install.ps1'  // Установочный скрипт для .NET
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Myakui/AvaloniaTest.git'
            }
        }
        stage('Setup .NET') {
            steps {
                script {
                    // Скачиваем .NET установочный скрипт для Windows
                    bat 'Invoke-WebRequest -Uri "https://dot.net/v1/dotnet-install.ps1" -OutFile "$env:DOTNET_INSTALL_SCRIPT"'
                    // Запуск установки .NET
                    bat "& .\\$env:DOTNET_INSTALL_SCRIPT -Version $env:DOTNET_VERSION"
                    // Добавляем .NET в PATH
                    bat '$env:PATH += ";$env:USERPROFILE\\.dotnet"'
                }
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
