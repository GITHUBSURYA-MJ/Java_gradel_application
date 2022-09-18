pipeline{
    agent any 
    stages{
       stage('SCM Checkout') {
            steps{
            git url: 'https://github.com/GITHUBSURYA-MJ/Java_gradel_application.git', branch: "main"
            }
        }

        stage('Build package') {
            steps{
                sh '/opt/gradle-6.8.3/bin/gradle clean build'
            }
        }

        stage('push to nexus') {
            steps {  
                  nexusArtifactUploader artifacts: [
                      [
                         artifactId: 'sampleWeb', 
                         classifier: '', 
                         file: 'build/libs/sampleWeb-0.0.1.war', 
                         type: 'war'
                     ]
               ], 
               credentialsId: 'nexus', 
               groupId: 'com.example', 
               nexusUrl: '172.31.27.85:8081', 
               nexusVersion: 'nexus3', 
               protocol: 'http', 
               repository: 'Gradle-release', 
               version: '0.0.1'
            }
        }
    }
}
