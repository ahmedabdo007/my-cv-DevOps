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
					def dockerCmd = 'docker run  -p 8080:80 -d  ahmedabdoahmed/cv-website:1.3'
						sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-184-73-148-149.compute-1.amazonaws.com ${dockerCmd}"
					}
                }
            }
        }
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
