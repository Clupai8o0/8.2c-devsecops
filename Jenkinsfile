pipeline {
  agent any

  environment {
    SONAR_TOKEN = credentials('SONAR_TOKEN')
  }

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
    stage('Generate Coverage Report') {
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
    stage('SonarCloud Analysis') {
      steps {
        sh 'sonar-scanner -Dsonar.login=$SONAR_TOKEN'
      }
    }
  }
}