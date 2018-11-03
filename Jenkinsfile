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
  }
}
