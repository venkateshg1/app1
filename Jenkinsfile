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
                 withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'dockerpasswd', usernameVariable: 'dockeruser')])  {
    
                 sh 'docker login -u ${dockeruser} -p ${dockerpasswd}'
                 sh 'docker push docker.io/venky3690/image:${BUILD_NUMBER}'
                }
                 
              }
           }
       stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
     sh "docker run -dt -p 9091:80 docker.io/venky3690/image:${BUILD_NUMBER}"
 
            }
        }
      }
}
