pipeline {
  agent any
     stages {
       stage ("maven") {
         steps 
            {
               sh 'mvn clean package'
            }
       }
       stage ("Build") { 
          steps
              { 
                 sh 'docker build -t docker.io/venky3690/image:${BUILD_NUMBER} -f Imagefiles/Dockerfile .'
 
              }
           }
       stage ("Push") {
          steps
              { 
                 withCredentials([usernamePassword(credentialsId: 'DockerCred', passwordVariable: 'dockerpasswd', usernameVariable: 'dockeruser')])  {
    
                 sh 'docker login -u ${dockeruser} -p ${dockerpasswd}'
                 sh 'docker push docker.io/venky3690/image:${BUILD_NUMBER}'
                }
                 
              }
           }
       stage('Run Docker container on Jenkins Agent') {
             
            steps 
             {
                 sh "docker run -dt -p 9094:80 docker.io/venky3690/image:${BUILD_NUMBER}"
             }
        }
       stage("Deploy to Kubernetes Cluster"){
            steps
         {
            sh 'kubectl apply -f Deploy.yml'
         }
       } 
      }
}
