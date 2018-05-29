pipeline {
  agent {
    docker {
    }
    stage('test') {
      environment {
        CI = 'True'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click \'Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
 
      }
    }
 
      image 'node:6-alpine'
      args '-p 6000:6000'
    }
  }
  
  triggers {
      pollSCM('H/10 * * * *') }
  stages {
    stage('install') {
      steps {
        sh 'npm install'
      } }

  }
