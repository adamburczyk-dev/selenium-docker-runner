pipeline {

    agent any

    parameters {
  choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
}


    stages {
        stage('Start Grid') {
            steps { 
                bat "docker-compose -f grid.yaml up --scale ${params.BROWSER}=1 -d"
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
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
            bat "docker compose -f grid.yaml down"
            bat "docker compose -f test-suites.yaml down"
    }
}
}