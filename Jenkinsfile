@Library('jenkins-shared-library') _


pipeline {   
    agent any
    tools {
        maven 'Maven'
    }
    stages {

        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage 'kachiie/demo-app:jma-3.0'
                    dockerLogin()
                    dockerPush 'kachiie/demo-app:jma-3.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                deployApp()
                }
            }
        }               
    
    }
}
