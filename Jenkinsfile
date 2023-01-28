pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git branch: 'main', credentialsId: 'GitCred', url: 'https://github.com/venkateshg1/app1.git'
            }
        }
        stage('Build') {
            steps {
               sh 'pwd'
               sh 'ls -l'
               sh 'mvn --version'
               sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
