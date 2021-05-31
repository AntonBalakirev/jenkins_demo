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
		success {
			emailext body: 'Status: Successful', 
				recipientProviders: [buildUser()], 
				subject: '[Jenkins] example_demo', 
				to: 'antonblkrv@gmail.com'
		}
		failure {
			emailext body: 'Status: Failure', 
				recipientProviders: [buildUser()], 
				subject: '[Jenkins] example_demo', 
				to: 'anton_balakirev@epage.ru'
		}
		cleanup {
			cleanWs notFailBuild: true
		}
	}
}
