library identifier: 'jenkins-shared-library@main', retriever: modernSCM(
        [$class:'GitSCMSource',
         remote: 'https://github.com/Titobid/Jenkins-shared-library.git',
         credentialsID: 'github-cred'])
def gv

pipeline {   
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
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
                    buildImage 'titobid/jenkins-app:2.0'
                    dockerLogin()
                    dockerPush 'titobid/jenkins-app:2.0'
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }               
    }
} 
