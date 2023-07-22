pipeline{
    agent none 
    environment { 
        demo = 'environment'
    }
    options { 
        buildDiscarder(logRotator(numToKeepStr: '3'))
        timeout(time: 1, unit: 'HOURS') 
         retry(3)
         }
    stages {
        stage ("clone"){
            agent any
            environment {
                stageenvironment = 'clone-stage'
                dockercreds = credentials("dockerhub")
            }
            steps{
                script {
                    currentBuild.displayName = env.JOB_NAME + "#" + env.BUILD_NUMBER
                    currentBuild.description = env.BRANCH_NAME
                    currentBuild.description = env.GIT_COMMIT

                    echo "This is clone stage."
                    sh 'printenv'
                    sh "docker login -u $dockercreds_USR -p $dockercreds_PSW"

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
            timeout(1) {
            
                script {
                    timeout(2) {
                    sh 'python --version'

                }

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
