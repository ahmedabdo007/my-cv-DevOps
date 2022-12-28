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

	post {
		always {
			sh 'docker logout'
		}
	}

}
