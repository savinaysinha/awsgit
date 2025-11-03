pipeline {
    agent any
    environment{
        PROJECT_NAME="SaviNetwork"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'echo "${PROJECT_NAME}"'
            }
        }
        stage('Deployment to TEST Env') {
            steps {
                echo 'Deployment to TEST Env'
            }
        }
         stage('Deployment to PROD Env') {
            input{
                 message('Proceed or Abort ?')
             }
            steps {
                echo 'Deployment to PROD Env'
            }
        }
    }
    post{
        always{
            echo 'Post Always'
        }
        aborted{
            echo 'Post Aborted'
        }
        success{
            echo 'Post Success'
        }
        failure{
            echo 'Post Failure'
        }
    }
}
