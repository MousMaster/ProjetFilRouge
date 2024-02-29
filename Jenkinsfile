pipeline {
    environment {
        IMAGE_NAME = "ic-webapp"
        APP_CONTAINER_PORT = "8080"
        DOCKERHUB_ID = "choco1992"
        DOCKERHUB_PASSWORD = credentials('dockerhub_password')
        ANSIBLE_IMAGE_AGENT = "registry.gitlab.com/robconnolly/docker-ansible:latest"
        IC_WEBAPP_SERVER_DEV = "127.0.0.1"
    }
    agent none
    stages {
        stage('Build image') {
            agent any
            steps {
                script {
                    sh 'docker build --no-cache -f ./sources/app/${DOCKERFILE_NAME} -t ${DOCKERHUB_ID}/$IMAGE_NAME:$IMAGE_TAG ./sources/app'
                }
            }
        }
        stage('Scan Image with SNYK') {
            agent any
            environment {
                SNYK_TOKEN = credentials('snyk_token')
            }
            steps {
                script {
                    // SNYK scanning steps
                }
            }
        }
        stage('Run container based on builded image') {
            agent any
            steps {
                script {
                    // Running container steps
                }
            }
        }
        stage('Test image') {
            agent any
            steps {
                script {
                    // Testing steps
                }
            }
        }
        stage('Clean container') {
            agent any
            steps {
                script {
                    // Cleaning container steps
                }
            }
        }
        stage('Login and Push Image on docker hub') {
            agent any
            steps {
                script {
                    // Docker login and push steps
                }
            }
        }
        stage('Build EC2 on AWS with terraform') {
            agent {
                docker {
                    image 'jenkins/jnlp-agent-terraform'
                }
            }
            environment {
                AWS_ACCESS_KEY_ID = credentials('aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials('aws_secret_access_key')
                PRIVATE_AWS_KEY = credentials('private_aws_key')
            }
            steps {
                script {
                    // Terraform steps
                }
            }
        }
        stage('Prepare Ansible environment') {
            agent any
            environment {
                VAULT_KEY = credentials('vault_key')
                PRIVATE_KEY = credentials('private_key')
                PUBLIC_KEY = credentials('public_key')
                VAGRANT_PASSWORD = credentials('vagrant_password')
            }
            steps {
                script {
                    // Ansible preparation steps
                }
            }
        }
        stage('Deploy DEV env for testing') {
            agent {
                docker {
                    image 'registry.gitlab.com/robconnolly/docker-ansible:latest'
                }
            }
            stages {
                // Nested stages for DEV deployment
            }
        }
        stage('Delete Dev environment') {
            agent {
                docker {
                    image 'jenkins/jnlp-agent-terraform'
                }
            }
            environment {
                AWS_ACCESS_KEY_ID = credentials('aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials('aws_secret_access_key')
                PRIVATE_AWS_KEY = credentials('private_aws_key')
            }
            steps {
                script {
                    // Deletion steps
                }
            }
        }
        stage('Deploy in PRODUCTION') {
            agent {
                docker {
                    image 'registry.gitlab.com/robconnolly/docker-ansible:latest'
                }
            }
            stages {
                // Stages for PRODUCTION deployment
            }
        }
    }
    post {
        always {
            script {
                // Clean up steps
                // slackNotifier invocation
            }
        }
    }
}
