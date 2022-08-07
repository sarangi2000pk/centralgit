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
                slackSend channel: 'youtubejenkins', message: 'job started'
            
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
                deploy adapters: [tomcat9(credentialsId: 'ashoktomcattest', path: '', url: 'http://13.212.170.7')], contextPath: '/app', war: '**/*.war'
               
            
                }
            }
        stage("Deploy on prod"){
            input {
                message "should we continue"
                ok "yes we should"
            }
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'ashoktomcatprod', path: '', url: 'http://18.141.214.198')], contextPath: '/app', war: '**/*.war'
                
            
                }
            }
        }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend channel: 'youtubejenkins', message: 'job success'
        }
        failure{
            echo "========pipeline execution failed========"
            slackSend channel: 'youtubejenkins', message: 'job failed'
        }
    }
}
