pipeline {
	
	agent any

	stages {

		stage("build") {

			steps {
				echo 'bulding the application...'
			}
		}

		stage("test") {

			steps {
				echo 'testing the application...'
			}
		}

		stage("deploy") {

			steps {
				echo 'deploying the application...'
			}
		}
	}
	post {
		always {
			cleanWs notFailBuild: true
		}
		success {
			emailext body: 'Status: Successful', 
				recipientProviders: [buildUser()], 
				subject: '[Jenkins] example_demo', 
				to: 'anton_balakirev@epage.ru'
		}
		failure {
			emailext body: 'Status: Failure', 
				recipientProviders: [buildUser()], 
				subject: '[Jenkins] example_demo', 
				to: 'anton_balakirev@epage.ru'
		}
	
	}
}
