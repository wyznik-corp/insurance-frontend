pipeline {
  agent none
  environment {
    FAVORITE_COLOR = 'RED'
  }  
  triggers {
    eventTrigger simpleMatch('hello-api-deploy-event')
  }
  stages {
    stage('Test') {
      when {
        beforeAgent true
        not { branch 'main' }
      }
      agent {
        kubernetes {
          yamlFile 'nodejs-pod.yaml'
        }
      }
      steps {
        container('nodejs') { 
          sh 'node --version'
        }
      }
    }
    stage('Main Branch Stages') {
      when {
        beforeAgent true
        branch 'main'
      }
      stages {
        stage('Build and Push Image') {
          steps {
            echo "FAVORITE_COLOR is $FAVORITE_COLOR"  
            echo "TODO - build and push image"
          }
        }
        stage('Deploy') {
          agent any
          environment {
            FAVORITE_COLOR = 'BLUE'
            SERVICE_CREDS = credentials('example-service-username-password')
          }
          options {
            timeout(time: 10, unit: 'SECONDS') 
          }
          input {
            message "Should we continue with deployment?"
          }
          steps {
            sh 'echo TODO - deploy to $FAVORITE_COLOR with SERVICE_CREDS: username=$SERVICE_CREDS_USR password=$SERVICE_CREDS_PSW'
          }
        }
      }
    }
  }
}
