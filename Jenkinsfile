pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
	 M2_HOME="/opt/apache-maven-3.8.4"
         M2='$M2_HOME/bin'
         PATH='$M2:$PATH'	
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
                            artifactId: 'WebApp', 
                            classifier: '', 
                            file: "target/WebApp-1.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus-user-credentials', 
                    groupId: 'lu.amazon.aws.demo', 
                    nexusUrl: '54.169.88.118:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'test-release', 
                    version: '1.0'
                    }
            }
        }
  }

