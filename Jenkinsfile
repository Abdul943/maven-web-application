pipeline {
    agent any

    tools
    {
          maven 'Maven_3.9.9'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'DevOpsNovemberBatch', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
                    
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}