pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-u $(id -u):$(id -g)' // Запуск контейнера от имени текущего пользователя
                }
            }
            steps {
                sh '''
                    # Изменить права на директорию кэша npm, если она существует
                    if [ -d "$HOME/.npm" ]; then
                        sudo chown -R $(id -u):$(id -g) $HOME/.npm
                    fi

                    # Проверка версии Node.js и npm
                    node --version
                    npm --version

                    # Установка зависимостей и сборка
                    npm ci
                    npm run build

                    # Показать список файлов
                    ls -la
                '''
            }
        }
    }
}
