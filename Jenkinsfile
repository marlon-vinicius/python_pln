pipeline {
    agent any

    environment {
        PATH = "C:\\Windows\\System32;C:\\Users\\Marlon\\AppData\\Local\\Programs\\Python\\Python312;C:\\Users\\Marlon\\AppData\\Local\\Programs\\Python\\Python312\\Scripts;${env.PATH}"
    }

    parameters {
        string(name: 'DISTANCIA', description: 'Limiar de distancia de busca.')
        string(name: 'PERGUNTA', description: 'Pergunta a ser feita')
    }

    stages {
       stage('Preparação do Ambiente') {
           steps {
                bat 'pip install -r requisitos.txt'
           }
        }

        stage('Execução do Teste Levenshtein') {
            steps {
                bat 'python levenshtein_teste.py'
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
                bat 'python chat_bot.py ${env.DISTANCIA} ${env.PERGUNTA}'
            }
        }
    }
}
