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
		stage('Build'){
			steps {
				//sh 'mvn --version'
			    // sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
         

			}
		}
		stage('test'){
			steps {
			
                echo "Test"
     	        
			}
		}
		stage('Integration Test'){
			steps {
			
     	        echo "Integration Test"

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
