pipeline {
	agent any 
	tools {
		maven 'local_maven'	
	}
		
	stages {
		stage ('Build') {
			steps {
				bat 'mvn clean package'
			}
	
			post {
				success {
					echo "Archiving the Artifacts"
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		stage ('Deploy to tomcat server'){
			steps {

				bat  'curl -T D:\\Jenkins\\Jenkins.war  http://localhost:8181/manager/text/deploy?path=/'
				// bat  'curl -T C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\build-n-deploy\\target\\devOpsWeb.war http://localhost:8181/manager/text/deploy?path=/'
			   
			}
		}		
	}
}
