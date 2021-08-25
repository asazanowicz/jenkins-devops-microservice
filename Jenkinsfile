pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} 
	post  {
		always {
			echo "Nice doning ..."
		}
		success {
			echo "Successed"
		}
		failure {
			echo "Failure"
		}
	}
}
