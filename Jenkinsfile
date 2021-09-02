node {
   def commit_id
   stage('Preparation') {
     checkout scm
     sh "git rev-parse --short HEAD > .git/commit-id"                        
     commit_id = readFile('.git/commit-id').trim()
   }
   stage('test') {
     nodejs(nodeJSInstallationName: 'nodejs') {
       sh 'npm install --only=dev'
       sh 'npm test'
     }
   }
   stage('docker build/push') 
     withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: params.JP_DockerMechIdCredential, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
	usr = mukeshdhamat
	pswd = Secure$$2021
	}
	docker.withRegistry("https://index.docker.io/v1/", params.JP_DockerMechIdCredential) {
	sh "docker login -u ${usr} -p ${pswd} https://index.dcoker.io/v1/"
	def	image = docker.build("com.att.sharedservices/tomee-uslmonitor")
	image.push 'latest'
	}   
   }
