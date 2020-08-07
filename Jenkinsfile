pipeline {
	agent any
	environment {
		DOCKER_REGISTRY='hub.docker.com/sadaithal'
		DOCKER_CREDS='training'
	}
	stages {
		stage("Build") {
			tools {
  				dockerTool 'docker'
			}
			steps {
				def git_ = git 'git@github.com:aithal23/hello-world-webapp.git'
				def commitId = git_.GIT_COMMIT
				sh 'pip install -r hello-world-webapp/requirements.txt'
				image = docker.build DOCKER_REGISTRY + ":latest"
				docker.withRegistry( '', DOCKER_CREDS ) {
            		image.push()
          		}
				sh 'curl -X POST <Incoming Webhook URL> -H "Content-Type: application/text" -d \'Project Name: hello-world-webapp \n Build Commit: ${commitId} \n Build Status: ${currentBuild.currentResult}\' ' 
			}
		}
	}
}