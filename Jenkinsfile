pipeline {
  agent any
      tools
    {
       maven "Maven"
    }
     stages {
        stage ("SCM") { 
          steps
              { 
                sh 'git clone https://github.com/venkateshg1/app1.git'
 
              }
           }
     stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
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
                 withCredentials([usernamePassword(credentialsId: 'DockerCred', passwordVariable: 'dockerregpasswd', usernameVariable: 'dockeruser')]) {
    
                 sh 'docker login -u ${dockeruser} -p ${dockerregpasswd}'
                 sh 'docker push docker.io/venky3690/image:${BUILD_NUMBER}'
                }
                 
              }
           }
       stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
                sh "docker run -d -p 9090:8080 image"
 
            }
        }
      }
}
