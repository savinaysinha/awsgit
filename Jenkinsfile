pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    environment{
        project_name="Demo.zip_expanded"
    }
    stages{
       stage("Unit Test"){
           steps{
               echo "====++++executing Unit Test++++===="
                sh 'ls'
               sh 'cd "${project_name}"'
               sh 'mvn test'
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
                sh 'cd "${project_name}"'
                sh 'mvn install'
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
                 deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '9896e19f-67a6-4a2f-9a65-2cd6b00ae41e', path: '', url: '3.111.32.58:8080')], contextPath: 'app', war: '**/*.war'
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
