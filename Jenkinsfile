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
  }
}
