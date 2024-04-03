pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }
        stage ('Deploy to tomcat server'){
            step{
                deploy adapters: [tomcat9(credentialsId: 'a81fb9dc-989f-41c5-8d26-376deee1a489', path: '', url: 'http://192.168.56.1:8181/')], contextPath: null, war: ''
            }
            
        }
    }
}
