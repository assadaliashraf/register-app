pipeline {
    agent any

    

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
      
        stage('Checkout from SCM') {
            steps {
                checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '79f1a91d-19ac-4204-b9ed-543a187855a5', url: 'https://github.com/assadaliashraf/register-app.git']])
            }
        }
      
        stage('Clean Workspace') {
            steps {
                sh 'mvn clean package'
            }
        }
      
       stage('Test Application') {
            steps {
                sh 'mvn test'
            }
        }
      
    }
}

