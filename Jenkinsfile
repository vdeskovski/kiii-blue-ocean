node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
		if (env.BRANCH_NAME == 'dev'){
			app = docker.build("vdeskovski/kiii-blue-ocean")
		}
		else{
			echo "Not BUILDING a docker image right now, since this is not dev branch"
		}
    }
    stage('Push image') {
		if (env.BRANCH_NAME == 'dev') {
			docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
				app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
				app.push("${env.BRANCH_NAME}-latest")
				// signal the orchestrator that there is a new version
			}
		}
		else{
			echo "Not PUSHING a docker image right now, since this is not dev branch"
		}
    }
}