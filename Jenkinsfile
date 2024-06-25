pipeline {
    agent any

    stages {
       stage('Preparação do Ambiente') {
           steps {
                powershell 'pip install -r requisitos.txt'
           }
        }

        stage('Execução do Teste Levenshtein') {
            steps {
                powershell 'python levenshtein_teste.py'
            }
        }

        stage('Verificação do Arquivo de Perguntas') {
            steps {
                script {
                    if (fileExists('perguntas.txt')) {
                        echo 'Arquivo perguntas.txt encontrado!'
                    } else {
                        error('Arquivo perguntas.txt não encontrado. Interrompendo o pipeline.')
                    }
                }
            }
        }

        stage('Execução do Chatbot') {
            steps {
                powershell 'python chat_bot.py'
            }
        }
    }
}
