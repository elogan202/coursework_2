pipeline { 
agent any  

stages 
{
    stage('Building image') {
        steps{
            script {
		app = docker.build("elogan202/coursework2")
                   }
	     }
    }

    stage('Push image') {
			steps {
					script {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("latest")
				}
		}
        }
    stage('Sonarqube') {
      environment {
        scannerHome = tool 'SonarQubeScanner'
     }
       steps {
            withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true 
         }
        }
      }	
    }
  }
}

