pipeline {
    agent any

        environment {
                APP_NAME = "register-app-pipeline"
                RELEASE = "1.0.0"
                DOCKER_USER = "astivirgo"
               
                IMAGE_NAME = "${DOCKER_USER}" +  "/" + "${APP_NAME}"
                IMAGE_TAG = "${RELEASE}" + "{BUILD_NUMBER}"
             }

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

      stage('Docker Build and Push') {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image=docker.build "${IMAGE_NAME}"
                    }
                    docker.withRegistry('',DOCKER_PASS) {
                      docker_image.push("${IMAGE_TAG}")
                      docker_image.push('latest')
                    }
                    
                }
            }
        }



    


        
      
    }
}

