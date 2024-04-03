pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps {
                script {
                    def warFile = findFiles(glob: '**/target/*.war')[0]
                    if (warFile != null) {
                        deploy adapters: [tomcat9(credentialsId: 'a81fb9dc-989f-41c5-8d26-376deee1a489', path: '', url: 'http://192.168.56.1:8181/')], 
                               contextPath: '/src/main/webapp', 
                               war: warFile.path
                    } else {
                        error "WAR file not found."
                    }
                }
            }
        }
    }
}
