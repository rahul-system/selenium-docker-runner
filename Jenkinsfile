pipeline{

    agent {

        label 'docker'

    }

    stages{

        stage('Run Test'){

            steps{
                bat "docker-compose up"

            }

        }

        stage('Bring Grid down'){

             steps{
                bat "docker-compose down"


            }

        }


            }

}