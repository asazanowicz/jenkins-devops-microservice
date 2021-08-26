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
			steps {
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
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				//"docker build -t asazanowicz/currency-exchange-devops:$env.BUILD_TAG"
				script  {
					dockerImage = docker.build("asazanowicz/currency-exchange-devops")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push("$env.BUILD_NUMBER")
						dockerImage.push('latest')
					}
				}
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
