node {
   environment {
     registry = "mukeshdhamat/nodejs"
     registryCredential = 'dockerhub_mukesh'
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
   stage('Docker Build') {
     agent any
     steps {
       sh 'docker build -t mukeshdhamat/nodejs:${commit-id} .'
       }
    }
   stage('Docker Push') {
     agent any
     steps {
       sh "docker login
       sh 'docker push mukeshdhamat/nodejs:${commit-id}'
     }
   }
}

