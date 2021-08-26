pipeline {
	agent any
	//agent { docker { image 'maven:latest' } }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin/:$dockerHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker --version'
				echo "PATH - $PATH"
				echo "BUILD_NUMBER = $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
			}
		}
		stage('Compile') {
			stages {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	} 
	post  {
		always {
			echo "$env.JOB_NAME is in progress ..."
		}
		success {
			echo "Successed"
		}
		failure {
			echo "Failure"
		}
	}
}
