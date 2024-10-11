pipeline{
	agent any
	stages{
		stage('Build'){
			steps{
				echo "Build"
			}
		}

		stage('Test'){
			steps{
				echo "Test"
			}
		}

		stage('Integration Test'){
			steps{
				echo "integration Test"
			}
		}
	} post {
		always {
			echo "Im awesome, i run always"
		}
		succes {
			echo "I run when you are successful"
		}
		failure {
			echo "I run when you fail"
		}
	}
}

