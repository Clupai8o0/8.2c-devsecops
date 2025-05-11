pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Clupai8o0/8.2c-devsecops.git'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm test || true' // allows pipeline to continue despite test failures
      }
    }
    stage('Generate Coverae Report') {
      steps {
        // Ensure coverage report exists
        sh 'npm run coverage || true'
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true' // This will show known CVEs in the output
      }
    }
  }
}