pipeline {
	agent any
	stages {
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
				echo "Integration Test"
			}
		}
	} post {
		always {
			echo "Im awseome. I run always"
		}
		success {
			echo "I run where when you aresuccessful"
		}
		failure {
			echo "I run when you fail"
		}
	}
	
}
