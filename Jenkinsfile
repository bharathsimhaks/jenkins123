pipeline {
    agent any
    environment {
        registry = "605176584238.dkr.ecr.us-east-1.amazonaws.com/myecr"
        dockerImageTag = "1.0" // Specify your desired tag here
    }
    stages {
        stage('Code Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'JenkinsGIT', url: 'https://github.com/bharathsimhaks/jenkins123.git']])
            }
        }
        stage('Building images') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${dockerImageTag}")
                }
            }
        }
        stage('Pushing to ECR') {
            steps {
                script {
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 605176584238.dkr.ecr.us-east-1.amazonaws.com"
                    sh "docker push ${registry}:${dockerImageTag}"
                }
            }
        }
    }
}
