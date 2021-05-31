CODE_CHANGES = true //some logic
pipeline {
	
	agent any
	
	environment {
		VERSION = '1.0'
	}

	stages {
		stage("build") {
			when {
				expression {
					env.BRANCH_NAME == 'main' && CODE_CHANGES == true
				}
			}
			steps {
				echo 'bulding the application...'
				echo "building version ${VERSION}"
			}
		}
		stage("test") {
			when {
				expression {
					(env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'main') && CODE_CHANGES == true
				}
			}
			steps {
				echo 'testing the application...'
				echo "testing version: ${VERSION}"
			}
		}
		stage("deploy") {
			when {
				expression {
					env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'main'
				}
			}
			steps {
				withCredentials([usernamePassword(credentialsId: 'MSemenovykh', passwordVariable: 'password', usernameVariable: 'username')]) {
					echo 'deploying the application...'
					echo "deploying version: ${VERSION}"
					echo "with credentials ${MSemenovykh}"
				}
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
