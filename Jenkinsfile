pipeline { 
agent any  

stages 
{
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
		app = docker.build("elogan202/coursework2")
			}
	 }
}
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("latest")
        }
    }
  }
}

