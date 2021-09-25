pipeline {
	//agent any
	agent { docker { image '3.8.2-jdk-11'} }
	stages{
		stage('Build'){
			steps {
				sh 'mvn --version'
				echo "Build"
         

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
