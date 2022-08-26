pipeline {
  environment {
    imagename = "priyappatil/maven2"
    registryCredential = 'priyappatil-dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/priya3019/priyaassign.git', branch: 'main'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Docker Run') {
     steps{
         script {
            dockerImage.run("-p 80605:8080 --rm --name priya123")
         }
     }
    }
    
    }
  }
