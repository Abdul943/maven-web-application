pipeline {
    agent any

    tools {
        maven 'Maven_3.9.9'
    }

    environment {
        buildNumber = "${build_Number}"
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
                sh "docker build -t abdul1992/login-service:${Build_Number} ."
            }
        }

        stage('Push Docker Image to DockerHub Repository') {
            steps {
                withCredentials([string(credentialsId: 'Docker_Hub_Password', variable: 'Docker_Hub_Password')]) {
                    sh "docker login -u abdul1992 -p ${Docker_Hub_Password}"
                }
                sh "docker push abdul1992/login-service:${build_Number}"
            }
        }
        stage('Remove Docker Image Locally In Jenkins')
        {
            steps
            {
                sh 'docker rmi abdul1992/login-service:${build_Number} '
            }
        }
    }
}