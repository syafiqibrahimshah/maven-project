pipeline {
    agent any

    tools {
      maven 'localMaven'
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package -DskipTests'
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
      }
  }
