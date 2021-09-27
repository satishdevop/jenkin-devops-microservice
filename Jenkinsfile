pipeline {
//	agent any
	agent { docker { image 'maven:3.6.3'} }
	//agent { docker { image 'node:current-alpine3.11'} }
    stages {
		stage('build') {
			steps {
				sh 'mvn --version'
				echo "build"
			}
		}
		stage('Integration Test') {
			steps {
				echo "test"
			}
		}
	}
        
	}
