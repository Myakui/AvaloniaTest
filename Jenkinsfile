pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'  // Версия .NET SDK
        PUBLISH_DIR = "/mnt/c/Users/yakov/Desktop/AvaloniaBuild"  // Путь для публикации на рабочем столе
    }
    stages {
        stage('Checkout') {
            steps {
                // Проверка и клонирование репозитория
                git branch: 'main', url: 'https://github.com/Myakui/AvaloniaTest.git'
            }
        }
        stage('Setup .NET') {
            steps {
                // Скачивание и установка .NET SDK
                sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                sh 'chmod +x dotnet-install.sh'
                sh './dotnet-install.sh --version $DOTNET_VERSION'
                sh 'export PATH=$HOME/.dotnet:$PATH'
            }
        }
        stage('Restore dependencies') {
            steps {
                // Восстановление зависимостей
                sh '$HOME/.dotnet/dotnet restore'
            }
        }
        stage('Build') {
            steps {
                // Сборка проекта
                sh '$HOME/.dotnet/dotnet build --configuration Release'
            }
        }
        stage('Test') {
            steps {
                // Запуск тестов
                sh '$HOME/.dotnet/dotnet test --configuration Release'
            }
        }
        stage('Publish') {
            steps {
                // Публикация сборки
                sh '$HOME/.dotnet/dotnet publish -c Release -o ./publish'
                // Копирование публикации в папку на рабочем столе
                sh 'cp -r ./publish/* $PUBLISH_DIR/'
            }
        }
    }
}
