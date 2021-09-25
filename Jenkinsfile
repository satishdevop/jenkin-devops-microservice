pipeline {
	agent any
	stages{
		stage('Build'){
			steps {
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
