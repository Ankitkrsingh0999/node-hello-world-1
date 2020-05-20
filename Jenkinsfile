pipeline {
  environment {
    dockerRegistry = "ankit0999/docker-nodejs"
    dockerRegistryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  tools {"node" }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/Ankitkrsingh0999/node-hello-world-1.git'
      }
    }
    stage('Build') {
       steps {
         sh 'npm install'
       }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build dockerRegistry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Upload Image') {
      steps{
        script {
          docker.withRegistry( '', dockerRegistryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $dockerRegistry:$BUILD_NUMBER"
      }
    }
  }
}
