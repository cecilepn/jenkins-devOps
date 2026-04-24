pipeline {
  agent any

  stages {
    stage('Install') {
      steps {
        sh 'npm ci' 
      } 
    }
    stage('Qualité') {
      parallel {
        stage('Lint') {
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
    // faire un build docker de cette image en utilisant le chemin de l'hôte 
    agent { dockerfile true } 
  }
}
