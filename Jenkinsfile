pipeline {

    agent any

    stages {
        stage('Run Test') {
            steps {
                bat "docker-compose up"
            }
        }
        stage('Bring Grid Down') {
            steps {
                bat "docker-compose down"
            }
        }
    }

    post {
        always {
            echo 'This will always run after the stages.'
        }
        success {
            echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
}