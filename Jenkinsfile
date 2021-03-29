pipeline {
  agent any

  stages {
     stage('Build') {
       steps {
         withCredentials([usernamePassword(credentialsId: "docker_credentials", usernameVariable: "username", passwordVariable: "pass")]) {
         sh 'docker build . -t omarquraah/nodejsapp:lts'
         sh 'echo $username'
         sh 'docker login -u $username -p $pass '
         sh 'docker push omarquraah/nodejsapp:lts'
         }
         
         post {
           success {
             slackSend(color: "33FFF3" , message:"build succeeded")
           }
         }
       }
     }
  
     stage('deploy') {
       steps {
         withCredentials([usernamePassword(credentialsId: 'docker_credentials', usernameVariable: 'username', passwordVariable: 'pass')]) {
         sh 'docker container run -d -p 3000:3000 omarquraah/nodejsapp:lts'
         }
       }
     }
  }
}

