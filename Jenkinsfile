pipeline{
    agent any 
    environment { 
        demo = 'environment'
    }
    options { 
        buildDiscarder(logRotator(numToKeepStr: '3'))
        timeout(time: 1, unit: 'MINUTES') 
        }
        parameters { 
            string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '') 
            choice(name: 'CHOICES', choices: ['one', 'two', 'three'], description: '')
            }
        triggers { 
            pollSCM('* * * * *')
            }
    stages {
        stage ("clone"){
            agent any
            environment {
                stageenvironment = 'clone-stage'
                dockercreds = credentials("docker_hub")
            }
            steps{
                script {
                    currentBuild.displayName = env.JOB_NAME + "#" + env.BUILD_NUMBER
                    currentBuild.description = env.BRANCH_NAME
                    currentBuild.description = env.GIT_COMMIT

                    echo "This is clone stage."
                    echo "$params.DEPLOY_ENV"
                    echo "$params.CHOICES"
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
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
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
            steps {
            
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
