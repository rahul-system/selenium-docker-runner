pipeline{

    agent any

    stages{

        stage('start grid'){

            steps{
                bat "docker-compose -f grid.yaml up -d"

            }

        }

        stage('Run Test'){

             steps{
                bat "docker-compose -f test-suite.yaml up"


            }

        }


            }

        post {

        always {

        bat "docker-compose -f grid.yaml down"
        bat "docker-compose -f test-suite.yaml down"
        }
        }

}