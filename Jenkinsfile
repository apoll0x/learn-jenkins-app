pipeline {
    agent any
    triggers {
    githubPush()
    }

    environment {
        NETLIFY_SITE_ID = '50548590-48f4-4ee2-8bb0-2212dbcbc2d8'
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
                agent {
                    docker {
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }
                
                steps {
                    sh '''
                        echo "Pora na testowanie.."
                        test -f build/index.html
                        npm test
                    '''
                }
            }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploy na produkcję. Site ID: $NETLIFY_SITE_ID"
                '''
            }
        }
        }



    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
