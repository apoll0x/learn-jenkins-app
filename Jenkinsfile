pipeline {
    agent any
    triggers {
    githubPush()
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Testowy komunikat! $JOB_NAME"
                    echo "Witaj, użytkowniku!"
                    echo "WRACAM!"
                    ls -la
                    echo "Sprawdzanie wersji node: "
                    node --version
                    echo "Sprawdzanie wersji npm: "
                    npm --version
                    echo "Uruchamianie npm, by móc buildować.."
                    npm ci
                    echo "Udało się! Budujemy.."
                    npm run build
                '''
            }
        }

    stage('Test') {
        steps {
            sh '''
                echo "Pora na testowanie.."
                test -f build/index.html
            '''
        }
    }
    }
}
