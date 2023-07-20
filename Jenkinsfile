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
            agent any
            steps{
                script {
                    echo "This is build stage."

                }

            }

        }
        stage ("test"){
            agent any 
            steps{
                script {
                    echo "This is test stage."

                }

            }

        }
    }
}
