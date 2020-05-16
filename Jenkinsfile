pipeline {
	// agent { docker {image 'maven:3.6.3'}}
	agent any 
	environment {
		dockerHome =tool 'myDocker'
		mavenHome= tool 'myMaven'
		PATH="$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout'){
			steps{  
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
								
				}
		}
		stage('Compile'){
			steps{
				sh "mvn clean compile"
				}
		}
		stage('Test'){
			steps{
				sh "mvn Test"
			}
		}
		stage('Integration Test'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package'){
			steps{
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image'){
			steps{
                 script{
					dockerImage= docker.build("8199/currency-exchange-devops:${env.BUILD_TAG}")
				 }
			}
		}

			stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('','dockerhub'){
                     dockerImage.push();
					dockerImage.push('latest');
					}
					
				}
			}
		}
	} 
	post {
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
