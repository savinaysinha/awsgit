pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    environment{
        PROJECT_NAME='Demo.zip_expanded'
        TEST_SERVER='http://43.204.228.242:8080'
        TEST_SERVER='http://43.204.228.242:8080'
        CONTEXT_PATH='app'
    }
    stages{
       stage("Unit Test"){
           steps{
               echo "====++++executing Unit Test++++===="
                dir(${PROJECT_NAME}) {
                    sh 'mvn test'
                }
           }
           post{
               always{
                   echo "====++++always++++===="
               }
               success{
                   echo "====++++Unit Test executed successfully++++===="
               }
               failure{
                   echo "====++++Unit Test execution failed++++===="
               }
       
           }
       }
        stage("Build"){
            steps{
                echo "====++++executing Build++++===="
                dir(${PROJECT_NAME}) {
                    sh 'mvn install'
                }
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++Build executed successfully++++===="
                }
                failure{
                    echo "====++++Build execution failed++++===="
                }
        
            }
        }
        stage("Deployment to Test Environment"){
            steps{
                echo "====++++executing Deployment to Test Environment++++===="
                 deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '9896e19f-67a6-4a2f-9a65-2cd6b00ae41e', path: '', url: ${TEST_SERVER})], contextPath: ${CONTEXT_PATH}, war: '**/*.war'
            }
            post{
                
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++Deployment to Test Environment executed successfully++++===="
                }
                failure{
                    
                    echo "====++++Deployment to Test Environment execution failed++++===="
                }
        
        
            }
        }
        stage("Deployment to Production Environment"){
            input {
                message 'Proceed for Production Deployment ?'
            }
            steps{
                echo "====++++executing Deployment to Production Environment++++===="
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++Deployment to Production Environment executed successfully++++===="
                }
                aborted{
                    echo "====++++Deployment to Production Environment execution failed++++===="
                }
                failure{
                    echo "====++++Deployment to Production Environment execution failed++++===="
                }
        
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
