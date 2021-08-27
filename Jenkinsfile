pipeline {
	triggers { cron('H 2 * * *') }
	options {
		buildDiscarder(logRotator(numToKeepStr: '10'))
		disableConcurrentBuilds()
		ansiColor('xterm')
	}
	agent {
		label 'docker'
	}
	environment {
		IMAGE = "docker.io/jc21/serverless:latest"
	}
	stages {
		stage('Build') {
			steps {
				ansiColor('xterm') {
					sh 'docker build --pull --no-cache --squash --compress -t ${IMAGE} .'
				}
			}
		}
		stage('Publish') {
			steps {
				withCredentials([usernamePassword(credentialsId: 'jc21-dockerhub', passwordVariable: 'dpass', usernameVariable: 'duser')]) {
					sh "docker login -u '${duser}' -p '${dpass}'"
					sh 'docker push ${IMAGE}'
				}
			}
		}
	}
	post {
		success {
			juxtapose event: 'success'
			sh 'figlet "SUCCESS"'
		}
		failure {
			juxtapose event: 'failure'
			sh 'figlet "FAILURE"'
		}
	}
}
