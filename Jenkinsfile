pipeline {
  agent any

  stages {
    stage('Install') {
      steps {
        sh 'npm ci' 
      } 
    }
    stage('Lint test') {
      steps {
        sh 'npm run lint' 
      } 
    }
    stage('Test') {
      steps {
        sh 'npm run test:coverage' 
      } 
    }
  }
}
