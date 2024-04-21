pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'D:/apache-maven-3.9.6/bin/mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps {
                script {
                    def warFile = findFiles(glob: '**.war')[0]
                    if (warFile != null) {
                        deploy adapters: [tomcat9(credentialsId: 'a81fb9dc-989f-41c5-8d26-376deee1a489', path: '', url: 'http://localhost:8181/')], 
                               contextPath: null, 
                               war: warFile.path
                    } else {
                        error "WAR file not found."
                    }
                }
            }
        }
    }
}
