pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 4000:4000'
    }
    
  }
  triggers {
      pollSCM('H * * * *') }
  stages {
    stage('install') {
      steps {
        sh 'npm install'
      }
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
  }
}
