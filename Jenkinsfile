pipeline {
  agent any
  tools { 
    maven 'Maven_3_5_2'  
  }
  stages {
    stage('CompileandRunSonarAnalysis') {
      steps {
        sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=aws-project-practice1 -Dsonar.organization=aws-project-practice1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=242ebbe0a6a08aa426ce2245d324e0125a2d5f64'
      }
    }
      
    stage('RunSCAAnalysisUsingSnyk') {
      steps {
        withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
          sh 'mvn snyk:test -fn'
        }
      }
    }

    stage('Build') {
      steps {
            withDockerRegistry([credentialsId: "dockerlogin", url: "" ])
            script{
                  app = docker.build("asg")
            }
      }
    }

    stage('Push') {
      steps {
            script{
                  docker.withRegistry('https://851725524822.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:aws-credentials'){
                        app.push("latest")
                  }
            }
      }
    }

  }
}
