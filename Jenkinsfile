pipeline {
  agent none
  stages {
    stage('Test') {
      agent { label 'nodejs-app' }
      steps {
        container('nodejs') {
          echo 'Hello World!'   
          sh 'node --version'
        }
      }
    }
    stage('Build and Push Image') {
      when {
        beforeAgent true
        branch 'main'
      }
      steps {
        echo "TODO - build and push image"
      }
    }
  }
}
