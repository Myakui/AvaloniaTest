pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'
        DOTNET_INSTALL_SCRIPT = 'dotnet-install.ps1'
        DOTNET_ROOT = "${env.USERPROFILE}\\.dotnet"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Myakui/AvaloniaTest.git'
            }
        }
        stage('Setup .NET') {
            steps {
                powershell '''
                    Invoke-WebRequest -Uri "https://dot.net/v1/dotnet-install.ps1" -OutFile "$env:DOTNET_INSTALL_SCRIPT"
                    powershell -ExecutionPolicy Bypass -File "$env:DOTNET_INSTALL_SCRIPT" -Version $env:DOTNET_VERSION
                '''
            }
        }
        stage('Restore') {
            steps {
                bat '"%USERPROFILE%\\.dotnet\\dotnet.exe" restore'
            }
        }
        stage('Build') {
            steps {
                bat '"%USERPROFILE%\\.dotnet\\dotnet.exe" build --configuration Release'
            }
        }
        stage('Test') {
            steps {
                bat '"%USERPROFILE%\\.dotnet\\dotnet.exe" test --configuration Release'
            }
        }
        stage('Publish') {
            steps {
                bat '"%USERPROFILE%\\.dotnet\\dotnet.exe" publish --configuration Release --output "%USERPROFILE%\\Desktop\\AvaloniaPublish"'
            }
        }
    }
}
