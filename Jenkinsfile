pipeline {
	agent any
	//agent { docker { image 'maven:3-openjdk-11'} }
	//agent { docker { image 'node:current-alpine3.11'} }

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage('checkout'){
			steps {
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
		stage ('compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
			
                sh "mvn test"
     	        
			}
		}
		stage('Integration Test'){
			steps {
			
     	        sh "mvn failsafe:integration-test failsafe:verify"

			}
		}

		stage('package') {
			steps {
			
     	        sh "mvn package -DskipTests"

			}
		}






		stage('Build Docker Image') {
			steps {
				//docker build -t skps27/currency-exchange-devops:$env.BUILD_TAG
				script {
					dockerImage = docker.build("skps27/currency-exchange-devops:${env.BUILD_TAG}")
				}
				
			}
		}
		stage('Push Docker Image') {
			steps {
			   script {
				   docker.withRegestry('','dockerhub') {
				   dockerImage.push();
				   dockerImage.push('latest');
				   }
			   }
			}
		}
	} 
	post {
		always {
			echo 'Iam awsome. I run always'
		}
		success {
			echo 'I run when ur are successful'
		}
		failure {
			echo 'I run when you fail'
		}
	}
        
	}
