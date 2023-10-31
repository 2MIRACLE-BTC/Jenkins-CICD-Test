pipeline {
 agent any
 environment {
 AWS_ACCOUNT_ID="822837196792"
 AWS_DEFAULT_REGION="ap-northeast-2" 
 IMAGE_REPO_NAME="test-ecr"
 IMAGE_TAG="latest"
 REPOSITORY_URI = "public.ecr.aws/r6s6v9h5/cicd-ecr"
 }
 
 stages {
 
 stage('Cloning Git') {
 steps {
 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/sd031/aws_codebuild_codedeploy_nodeJs_demo.git']]]) 
 }
 }

 // Building Docker images
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
 }
 }
 }

 stage('Logging into AWS ECR') {
 steps {
 script {
 sh "aws ecr get-login-password - region ${AWS_DEFAULT_REGION} | docker login - username AWS - password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
 }
 
 }
 }
 
