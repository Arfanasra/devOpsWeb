pipeline{
    agent any
    tools{
        maven 'local_maven'
    }
    stages{
        stage ('Build'){
            steps{
                bat 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'a81fb9dc-989f-41c5-8d26-376deee1a489', path: '', url: 'https://localhost:8181')], contextPath: null, war: '**.*.war'
            }
        }
    }
}
