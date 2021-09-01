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
   stage('docker build/push') {
     sh 'docker login -u mukeshdhamat -p Secure$$2021'
     sh 'docker build -t mukeshdhamat:${commit_id}'
     sh 'docker push mukeshdhamat:${commit_id}'
     }
   }

