pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Informative Checkouts') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH" // Corrected case
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}

		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}

		stage('Test') {
			steps {
				echo "mvn test"
			}
		}

		stage('Integration Test') {
			steps {
				echo "mvn failsafe:integration-test failsafe:verify" // Fixed typo here
			}
		}

		stage('package'){
			steps{
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image') {
			steps {
				script{
					dockerImage = docker.build("hrushertz/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('', 'Docker'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
	} 
	
	post {
		always {
			echo "I'm awesome, I run always"
		}
		success {
			echo "I run when you are successful"
		}
		failure {
			echo "I run when you fail"
		}
	}
}
