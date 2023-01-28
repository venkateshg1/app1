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
               sh 'mvn --version'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
