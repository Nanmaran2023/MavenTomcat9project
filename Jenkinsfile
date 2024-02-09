pipeline {
	agent any	
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	
	stage('Build'){
		steps{
			sh "mvn clean install -Dmaven.test.skip=true"
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	
	stage('deployment'){
		steps{
		deploy adapters: [tomcat(url: 'http://localhost:8081/',credentialsId: 'tomcat')], 
                     war: 'target/*.war',
                     contextPath: 'app'
		}
		
	}
	}
}
