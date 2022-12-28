pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-hub-repo')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t ahmedabdoahmed/cv-website:1.3 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}


		stage('Push') {

			steps {
				sh 'docker push ahmedabdoahmed/cv-website:1.3'
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

	post {
		always {
			sh 'docker logout'
		}
	}

}
