#!/usr/bin/env groovy

pipeline {
    agent none
    stages {
        stage('build') {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image ..."
                    withCredentials([usernamePassword(cerdintialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER' )])
                        sh 'docker build -t ahmedabdoahmed/cv-website:cv-1.0 .'
                        sh "echo $PASS | doocker login -u $USER --password-stdin"
                        sh 'docker push ahmedabdoahmed/cv-website:cv-1.0'
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
