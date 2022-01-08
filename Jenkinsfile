pipeline {
    agent any
    tools {
        maven 'maven'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-web-app', 
                            classifier: '', 
                            file: "target/simple-web-app-1.0.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus-user-credentials', 
                    groupId: 'org.mitre', 
                    nexusUrl: '54.169.88.118:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'test-release', 
                    version: '1.0.0'
                    }
            }
        }
  }

