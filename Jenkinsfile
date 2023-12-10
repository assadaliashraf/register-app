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
                checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '79f1a91d-19ac-4204-b9ed-543a187855a5', url: 'https://github.com/assadaliashraf/register-app.git']])
            }
        }
      
        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }
      
       stage('Test Application') {
            steps {
                sh 'mvn test'
            }
        }

 /*    stage("SonarQube Analysis"){
           steps {
	           script {
		        withSonarQubeEnv(credentialsId: 'Jenkins-sonarqube-token') { 
                        sh "mvn sonar:sonar"
		        }
	           }	
           }
       } */

	stage("Quality Gate"){
           steps {
	           script {
		           waitForQualityGate abortPipeline: false, credentialsId: 'Jenkins-sonarqube-token'
		        }
	           }	
           }
           




        
      
    }
}

