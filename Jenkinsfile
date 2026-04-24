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
    stage('build Docker image') {
      steps {
          sh 'docker build jenkins/jenkins:lts'
          sh 'echo "Build OK"'
      }
    }
  }
}