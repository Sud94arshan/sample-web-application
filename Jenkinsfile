pipeline{
    agent none

    stages {
        stage ("clone"){
            agent any
            steps{
                script {
                    echo "This is clone stage."

                }

            }

        }
        stage("build"){
            agent {
                docker {
                    image 'python:3.7-buster'
                    
                }
            }
            steps{
                script {
                    sh 'python --version'

                }

            }

        }
        stage ("test"){
            agent {
                docker {
                    image 'python:3.9-buster'
                    
                }
            }
            steps{
                script {
                    sh 'python --version'

                }

            }

        }
    }
}
