pipeline {
	//agent any
	agent { docker { image 'maven:latest' } }
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
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
