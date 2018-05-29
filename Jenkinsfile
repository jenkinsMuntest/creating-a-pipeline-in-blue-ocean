pipeline {
  agent {
    docker {
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
        
      post {
       // only triggered when blue or green sign
       success {
           slackSend channel: '#thethingbroke',
             		 color: 'good',
             message: "The pipeline ${currentBuild.fullDisplayName} Completed"
       }
       // triggered when red sign
       failure {
           slackSend channel: '#thethingbroke',
             		 color: 'bad',
             message: "The pipeline ${currentBuild.fullDisplayName} Completed"
       }
       // trigger every-works
       always {
           slackSend channel: '#thethingbroke',
             		 color: 'good',
             message: "The pipeline ${currentBuild.fullDisplayName} Completed"
       }
    }
      }
    }
  }
}
