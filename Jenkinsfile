pipeline{
    agent none 
    environment {
        demo = 'environment'
    }

    stages {
        stage ("clone"){
            agent any
            steps{
                script {
                    echo "This is clone stage."
                    sh 'printenv'

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
    post {
        always {
            cleanWs()
        }
        failure {
            echo "pipeline failed will be sending failure mail."
        }
    }
}
