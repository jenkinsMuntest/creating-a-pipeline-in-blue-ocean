pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'npm install'
          }
        }
        stage('touch') {
          steps {
            sh 'touch test.txt'
          }
        }
        stage('') {
          steps {
            sh 'rm test.txt'
          }
        }
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