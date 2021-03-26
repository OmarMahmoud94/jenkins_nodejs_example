pipeline {
  agent any

  stages {
     stage('Build') {
       steps {
         withCredentials([usernamePassword(credentialsId: 'docker_credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
         sh 'docker build . -t omarquraah/nodejsapp:lts'
         sh 'docker login -u $(USERNAME) -p $(PASSWORD) '
         sh 'docker push omarquraah/nodejsapp:lts'
         }
       }
     }
  
     stage('deploy') {
       steps {
         withCredentials([usernamePassword(credentialsId: 'docker_credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
         sh 'docker container run -d -p 3000:3000 omarquraah/nodejsapp:lts'
         }
       }
     }
  }
}

