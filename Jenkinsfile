pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'JDK'
    }
    environment {
        AWS_ACCOUNT_ID="461706885282"
        AWS_DEFAULT_REGION="us-west-1" 
        IMAGE_REPO_NAME="multi"
        IMAGE_TAG= "latest"
        REPOSITORY_URI = "${461706885282}.dkr.ecr.${us-west-1}.amazonaws.com/${multi}"
    }
   
    stages {
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                sh "aws ecr get-login-password --region ${us-west-1} | docker login --sharan9611 AWS --madhurani@24-stdin ${461706885282}.dkr.ecr.${us-west-1}.amazonaws.com"
                }
                 
            }
        }
        
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/dev']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/sharan9611/multi-stage-example.git']]])     
            }
        }
         stage('Maven Build') {
            steps {
               sh "mvn clean package" 
            }
        }
  
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build "${multi}:${latest}"
        }
      }
    }
   
    // Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
     steps{  
         script {
                sh "docker tag ${multi}:${latest} ${https://github.com/sharan9611/multi-stage-example.git}:${latest}"
                sh "docker push ${461706885282}.dkr.ecr.${us-west-1}.amazonaws.com/${multi}:${latest}"
}
         }
        }
      }
    }

