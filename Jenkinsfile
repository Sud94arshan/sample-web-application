pipeline{
    agent any 
    environment { 
        demo = 'environment'
    }

    stages {
        stage ("clone"){
            agent any
            environment {
                stageenvironment = 'clone-stage'
                
            }
            steps{
                script {
                    currentBuild.displayName = env.JOB_NAME + "#" + env.BUILD_NUMBER
                    currentBuild.description = env.BRANCH_NAME
                    currentBuild.description = env.GIT_COMMIT
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
                    sh 'printenv'

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
