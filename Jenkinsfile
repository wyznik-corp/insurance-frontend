pipeline {
  agent none
  environment {
    FAVORITE_COLOR = 'RED'
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
          environment {
            FAVORITE_COLOR = 'BLUE'
          }
          steps {
            echo "TODO - deploy to $FAVORITE_COLOR"
          }
        }
      }
    }
  }
}
