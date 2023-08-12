pipeline {
    agent any
    tools{
        maven 'maven_3_9_4'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/tuhocdevops/devops-automation']])
                sh 'mvn clean install' 
            }
        }    
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t java-test:v1 .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                    sh 'docker login -u iamjohnny95 -p ${dockerhub}'
                    
                        
}
                    sh 'docker image tag java-test:v1 iamjohnny95/app-java'
                    sh 'docker image push iamjohnny95/app-java:v1'

                }
            }
        }    
    }    
}