/* import shared library. */

pipeline {
    environment {
        IMAGE_NAME = "ic-webapp"
        APP_CONTAINER_PORT = "8080"
        DOCKERHUB_ID = "mous172782"
       // DOCKERHUB_PASSWORD = credentials('dockerhub_password')
        //DOCKERHUB_PASSWORD = "jdj"
        ANSIBLE_IMAGE_AGENT = "registry.gitlab.com/robconnolly/docker-ansible:latest"
        IC_WEBAPP_SERVER_DEV = "127.0.0.1"
    }
    agent none
    stages {
    
        stage('Build image') {
           agent any
           steps {
              script {
                sh 'docker build -t $IMAGE_NAME ./sources/app'
              }
           }
        }
    }
    
}