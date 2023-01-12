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
                   echo 'deploying docker image to ec2...'
                   def ansibleCmd = "ansible-playbook ansible-playbook.yml"
                   sshagent(['ec2-server-key']) {
					sh "scp ansible-playbook.yml ubuntu@ec2-184-73-148-149.compute-1.amazonaws.com:/home/ubuntu"
						sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-184-73-148-149.compute-1.amazonaws.com ${ansibleCmd}"
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
