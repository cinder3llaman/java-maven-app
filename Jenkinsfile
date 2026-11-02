pipeline {   
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application...."
                    echo "Testing the integration...."
                }
            }
        }
        
        stage("build") {
            steps {
                script {
                    echo "Building the application...."
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    def dockerCmd = 'docker run -p 3080:3080 -d kachiie/demo-app:jma-2.0'
                    sshagent(credentials: ['ec2-server-key'], executable: '') {
   sh "ssh -o StrictHostKeyChecking=no ec2-user@3.128.254.215 ${dockerCmd}"
}
                }
            }
        }               
    }
} 
