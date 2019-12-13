pipeline { 
agent any  

stages 
{
	stage('Building image') 
	{
		steps
		{
			script 
			{
				app = docker.build("elogan202/coursework2")
			}
		}
	}

	stage('Push image') 
	{
		steps 
		{
			script 
			{
				docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials')
				{
					app.push("latest")
				}
			}
		}
        }


	stage('Sonarqube')
	{
		environment
		{
			scannerHome = tool 'SonarQubeScanner'
		}
			steps
			{
				withSonarQubeEnv('SonarQube')
				{
					sh "${scannerHome}/bin/sonar-scanner"
				}
			}
	}	
	stage('Deploy Update')
	{
		steps
		{
			sh 'ssh -t azureuser@13.82.193.106 kubectl set image deployments/kubernetes/latest serverjs=elogan202/serverjs:v10'
		}
	}
}
	}

