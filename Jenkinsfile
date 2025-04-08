pipeline {
    agent any

    environment {
        SOLUTION = 'AvaloniaTest.sln'
        PROJECT = 'AvaloniaTest.csproj'
        CONFIGURATION = 'Release'
        PLATFORM = 'x64'
    }

    stages {
        stage('Clean workspace') {
            steps {
                cleanWs()
            }
        }



        stage('Restore') {
            steps {
                bat "dotnet restore ${env.SOLUTION}"
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build AvaloniaTest.sln -c Release'
                script {
                    if (currentBuild.result == 'FAILURE') {
                        error("Build failed!")
                    }
                }
            }
        }

        stage('Publish') {
            steps {
                bat 'dotnet publish %SOLUTION% -c Release -r win-x64 --self-contained'
                script {
                    if (currentBuild.result == 'FAILURE') {
                        error("Publish failed!")
                    }
                }
            }
        }

        stage('Tests (skipped)') {
            steps {
                echo 'Нет проекта с тестами. Пропускаем.'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/bin/x64/Release/net9.0/win-x64/publish/**', allowEmptyArchive: true
        }
    }
}
