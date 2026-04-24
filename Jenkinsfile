pipeline {
  agent any

  stages {
    stage('Install') {
      steps {
        sh 'npm ci' 
      } 
    }
    stage('Tests') {
      steps {
        sh 'npm run lint && npm run test:coverage' 
      } 
    }
  }
}
