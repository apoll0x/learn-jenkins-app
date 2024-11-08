pipeline {
    agent any
    triggers {
    githubPush()
    }

    stages {
        stage('Hello') {
            steps {
                sh '''
                echo "Testowy komunikat! $JOB_NAME"
                echo "Witaj, użytkowniku!"
                '''
            }
        }
    }
}
