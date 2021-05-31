def CODE_CHANGES = true //declare local params

pipeline {
	
	agent any
	
	triggers { 
		cron('H(30-35) 8 * * 1-5') 
	}
	
	environment {
		ENV = 'Linux'
	}
	
	parameters {
		choice(name: 'VERSION', choices: ['1.0', '2.0', '3.0'], description: 'version to deploy')
		booleanParam(name: 'TEST', defaultValue: true, description: '')
	}
	
	tools {
		maven '3.6.3'
	}

	stages {
		stage("init") {
			steps {
				echo "branch name: ${env.BRANCH_NAME}"
				echo "env: ${ENV}"
				// sh 'mvn clean'
			}
		}
		stage("build") {
			when {
				expression {
					env.BRANCH_NAME == 'main' && CODE_CHANGES == true
				}
			}
			steps {
				echo 'bulding the application...'
				echo "building version ${params.VERSION}"
			}
		}
		stage("test") {
			when {
				expression {
					params.TEST == true
				}
			}
			steps {
				echo 'testing the application...'
				echo "testing version: ${params.VERSION}"
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
					echo "deploying version: ${params.VERSION}"
					echo "with credentials ${params.MSemenovykh}"
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
