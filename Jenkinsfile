pipeline {
  agent any

  options {
    disableConcurrentBuilds() // interdit le fait de lancer ce job 2 fois en même temps 
    parallelsAlwaysFailFast // dans un parallel, si un test échoue, tout s'arrête 
  }

  environment {
    IMAGE_NAME = "app-test"
  }

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
          sh '''
          docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .
          docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest
          '''
      }
    }
    stage('Deploy') {
      steps {
          sh 'docker run -d -p 3002:3000 ${IMAGE_NAME}:${IMAGE_NUMBER}'
      }
    }
    stage('Test') {
      steps {
          sh 'curl host.internal.docker:3000/health'
      }
    }
  }
}