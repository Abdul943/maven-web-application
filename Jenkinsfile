pipeline {
    agent any

    tools {
        maven 'Maven_3.9.9'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'DevOpsNovemberBatch',
                    url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t abdul1992/login-service:${BUILD_NUMBER} ."
            }
        }

        stage('Push Docker Image to DockerHub Repository') {
            steps {
                withCredentials([string(credentialsId: 'Docker_Hub_Password', variable: 'PASS')]) {
                    sh "echo ${PASS} | docker login -u abdul1992 --password-stdin"
                }
                sh "docker push abdul1992/login-service:${BUILD_NUMBER}"
            }
        }

        stage('Remove Docker Image Locally In Jenkins') {
            steps {
                sh "docker rmi abdul1992/login-service:${BUILD_NUMBER}"
            }
        }
    }
}