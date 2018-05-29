pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 6000:6000'
    }
    
  }
  triggers {
      pollSCM('H/5 * * * *') }
   post {
       // only triggered when blue or green sign
       success {
           slackSend channel: '#thethingbroke',
             		 color: 'good',
             message: "The pipeline ${currentBuild.fullDisplayName} Completed and successful"
       }
       // triggered when red sign
       failure {
           slackSend channel: '#thethingbroke',
             		 color: 'danger',
             message: "The pipeline ${currentBuild.fullDisplayName} Failed, Please review changes"
       }
       
       }
    
  stages {
    stage('install') {
      steps {
        sh 'nm install'
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
      }
    }
  }
}
