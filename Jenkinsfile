pipeline {
    agent any 
    tools {
maven 'Maven'
    }
    stages {
        stage('Build jar') {
            steps {
                echo 'Building the application...'
                sh 'mvn package'
            }
        }
            stage('Build image') {
            steps {
                script{
                echo 'Building the docker image...'
                    withCredentials([usernamePassword(credentialsId:'docker-hub-repo',PasswordVariable: 'PASS', usernameVariable:'USER')]) {
               sh 'docker build -t kachiie/demo-app:jma-2.0 .'
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push kachiie/demo-app:jma-2.0'
                }
                sh 'mvn package'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
            }
        }
    }
}
