pipeline{
    agent any 
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages{
       stage('SCM Checkout') {
            steps{
            git url: 'https://github.com/InnaPavan/Java_gradel_application.git', branch: "main"
            }
        }

        stage('Build package') {
            steps{
                sh './gradlew clean build'
            }
        }

        stage('push to nexus') {
            steps {  
                  nexusArtifactUploader artifacts: [
                      [
                         artifactId: 'spring-petclinic', 
                         classifier: '', 
                         file: 'build/libs/spring-petclinic-${VERSION}.war', 
                         type: 'war'
                     ]
               ], 
               credentialsId: 'nexus', 
               groupId: ''com.example, 
               nexusUrl: '172.31.41.122.69:8081', 
               nexusVersion: 'nexus3', 
               protocol: 'http', 
               repository: 'maven-releases', 
               version: '${VERSION}'
            }
        }
    }
}
