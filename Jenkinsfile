pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=mubuddywebapp -Dsonar.organization=mubuddywebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=a2bfec8154873220d88d9bec5877e14cc9df5a14'
			}
        } 
  }
}
