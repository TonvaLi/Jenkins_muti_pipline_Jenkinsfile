#!groovy
#!groovy
pipeline {
    agent none
    stages {
         	stage('Build'){
            agent any
            steps {
                checkout scm
                sh 'make'
                stash includes: '**/target/*.jar', name: 'app' 
            }
        }
         	stage('Test on master') {
            agent { 
                label 'tester_wsr'
            }
            steps {
                unstash 'app' 
                sh 'make check'
            }
            post {
                always {
                    junit '**/target/*.xml'
                }
            }
        }
         	stage('Test on mac_tt') {
            agent {
                label 'tester_tt'
            }
            steps {
                unstash 'app'
                bat 'make check' 
            }
            post {
                always {
                    junit '**/target/*.xml'
                }
            }
        }
    }
}
