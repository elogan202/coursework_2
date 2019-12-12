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
    }
  }
}

