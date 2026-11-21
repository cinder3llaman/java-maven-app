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
            withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                def dockerCmd = "echo ${PASS} | docker login -u ${USER} --password-stdin && docker run -p 3080:3080 -d kachiie/demo-app:jma-2.0"
                sshagent(['ec2-server-key']) {
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@3.151.140.160 '${dockerCmd}'"
                }
            }
        }
    }
}
    }
