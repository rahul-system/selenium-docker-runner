pipeline{

    agent any

    parameters {
      choice choices: ['chrome', 'firefox'], description: 'choose the browser', name: 'BROWSER'
    }

    stages{

        stage('start grid'){

            steps{
                bat "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"

            }

        }

        stage('Run Test'){

             steps{
                bat "docker-compose -f test-suite.yaml up --pull=always"
                script {
                    if(fileExists('output/flight-reservation/testng-failed.xml') || fileExists('output/vendor-portal/testng-failed.xml')) {
                        error('failed tests found')
                    }
                }


            }

        }
    }

    post {

        always {
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suite.yaml down"
            archiveArtifacts artifacts: '/output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: '/output/flight-reservation/emailable-report.html', followSymlinks: false
        }
    }

}