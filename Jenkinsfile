node {
    def newApp
    def registry = 'https://registry-1.docker.io/v2/'
	def imagename = "amuyal/todo"
    def registryCredential = 'dockerhub'

	stage('Git') {
		git 'https://github.com/amuyal/node-todo-frontend.git'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( registry, registryCredential ) {
		    def buildName = imagename + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
}
