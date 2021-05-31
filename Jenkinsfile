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
			mail bcc: '', 
				body: 'Status: Successful', 
				cc: '', 
				from: 'Jenkins demo run', 
				replyTo: '', 
				subject: '[Jenkins] demo', 
				to: 'anton_balakirev@epage.ru'
		}
		failed {
			mail bcc: '', 
				body: 'Status: Failed', 
				cc: '', 
				from: 'Jenkins demo run', 
				replyTo: '', 
				subject: '[Jenkins] demo', 
				to: 'anton_balakirev@epage.ru'
		}
	
	}
}
