pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('build') {
      parallel {
        stage('install') {
          steps {
            sh 'npm install'
          }
        }
        stage('filemaker') {
          steps {
            sh './filemaker.sh'
          }
        }
      }
    }
    stage('test') {
      parallel {
        stage('test') {
          environment {
            CI = 'True'
          }
          steps {
            sh './jenkins/scripts/test.sh'
          }
        }
        stage('file test') {
          steps {
            sh './filetester.sh'
          }
        }
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