#!/usr/bin/env groovy

pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }
        stage('test') {
            steps {
                script {
                    echo "Testing the application..."
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                   sshagent(['ec2-server-key']) {
					def dockerCmd = 'docker run  -p 8082:80 -d  ahmedabdoahmed/cv-website:1.2'
						sh "ssh -o StrictHostKeyChecking=no ec2-user@ec2-3-88-225-211.compute-1.amazonaws.com ${dockerCmd}"
					}
                }
            }
        }
    }
}
