pipeline {
  agent any
     stages {
       stage ("Build") { 
          steps
              { 
                 sh 'docker build -t docker.io/venky3690/image:${BUILD_NUMBER} -f Imagefiles/Dockerfile .'
 
              }
           }
       stage ("Push") {
          steps
              { 
                 withCredentials([usernamePassword(credentialsId: 'DockerCred', passwordVariable: 'dockerregpasswd', usernameVariable: 'dockeruser')]) {
    
                 sh 'docker login -u ${dockeruser} -p ${dockerregpasswd}'
                 sh 'docker push docker.io/venky3690/image:${BUILD_NUMBER}'
                }
                 
              }
           }
       stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
     sh "docker run -dt -p 9093:80 docker.io/venky3690/image:${BUILD_NUMBER}"
 
            }
        }
      }
}
