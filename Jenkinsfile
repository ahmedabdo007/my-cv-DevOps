pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-hub-repo')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t ahmedabdoahmed/cv-website:1.4 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}


		stage('Push') {

			steps {
				sh 'docker push ahmedabdoahmed/cv-website:1.4'
			}
		}
        stage('deploy') {
            steps {
                script {
                   sshagent(['ec2-server-key']) {
					def dockerCmd = 'docker run  -p 8080:80 -d  ahmedabdoahmed/cv-website:1.4'
						sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-3-246-119.compute-1.amazonaws.com ${dockerCmd}"
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
