pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/maeve-g/8.2CDevSecOps.git'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm test || true'  
      }
      post {
        always {
          emailext(
            to: 's222237672@deakin.edu.au',
            subject: "Run Tests - ${currentBuild.currentResult}",
            body: "The Run Tests stage has finished with status: ${currentBuild.currentResult}",
            attachLog: true
          )
        }
      }
    }
    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
      post {
        always {
          emailext(
            to: 's222237672@deakin.edu.au', 
            subject: "Security Scan - ${currentBuild.currentResult}",
            body: "The Security Scan stage has finished with status: ${currentBuild.currentResult}",
            attachLog: true
          )
        }
      }
    }
  }
}
