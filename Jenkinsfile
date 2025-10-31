pipeline {

    agent any

    stages {
        stage('Start Grid') {
            steps {
                bat "docker-compose -f grid.yaml up -d"
            }
        }
        stage('Run Test Suites') {
            steps {
                bat "docker-compose -f test-suites.yaml up"
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
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
            archiveArtifacts 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}