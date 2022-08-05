pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
                
            
                }
            }
        stage("Build"){
            steps{
                sh "mvn package"
                
            
                }
            }
        stage("Deploy on test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'ashoktomcattest', path: '', url: 'http://13.229.151.30')], contextPath: '/app', war: '**/*.war'
               
            
                }
            }
        stage("Deploy on prod"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'ashoktomcatprod', path: '', url: 'http://18.140.130.83')], contextPath: '/app', war: '**/*.war'
                
            
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
