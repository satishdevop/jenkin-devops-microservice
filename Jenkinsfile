pipeline {
	agent any
	//agent { docker { image 'maven:3-openjdk-11'} }
	//agent { docker { image 'node:current-alpine3.11'} }

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		DOCKERHUB_CREDENTIALS = credentials('dockerhub')
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
				/*script {
					dockerImage = docker.build("skps27/currency-exchange-devops:${env.BUILD_TAG}")
				}*/
				sh 'docker build -t skps27/currency-exchange-devops:0.0.1'
				
			}
		}
        stage('login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
		stage('Push') {
			steps {
				sh 'docker push skps27/currency-exchange-devops:0.0.1'
			}
		}
		/*stage('Push Docker Image') {
			steps {
			   script {
				   docker.withRegistry('', 'dockerhub') {
				   dockerImage.push();
				   dockerImage.push('latest');
				   }
			   }
			}
		}*/

		/*stage('Push Docker Imnage') { 

            steps { 

                script { 

                    docker.withRegistry( '', 'dockerhub') { 

                        dockerImage.push() 

                    }

                } 

            }

        } */



	} 
	post {
		always {
			sh 'docker logout'
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
