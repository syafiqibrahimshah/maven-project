pipeline {
  agent any

  tools {
    maven 'localMaven'
  }

  stages {
    stage('Build'){
      steps {
        sh 'mvn clean package -DskipTests'
      }
      post {
        success {
          echo 'Now archiving...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }

    stage('Deploy to Staging'){
      steps {
        build job: 'Deploy-to-staging'
      }
    }

    stage('Deploy to Production'){
      steps {
        timeout(time:5, unit:'DAYS'){
          input message:'Approve Production Deployment?'
        }

        build job: 'Deploy-to-prod'
      }
      post {
        success {
          echo 'Code deployed to Production.'
        }
        failure {
          echo 'Deployment failed.'
        }
      }
    }
  }
}
