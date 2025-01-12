pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=aws-project-practice1 -Dsonar.organization=aws-project-practice1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=242ebbe0a6a08aa426ce2245d324e0125a2d5f64'
			}
        } 
      
      stage('RunSCAAnalysisUsingSnyk'){
            steps {
                  withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SYNK_TOKEN')]){
                        sh 'mvn synk:test -fn --org=karthikravi123 --project=aws-devsecops-repo-for-buildspec-with-sonarcloud --token=${SNYK_TOKEN}'
                  }
            }

      }

  }

  
}
