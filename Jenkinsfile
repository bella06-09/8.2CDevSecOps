pipeline {
  agent any
  environment {
    PATH = "/opt/homebrew/opt/node@18/bin:/opt/homebrew/bin:/usr/local/bin:${env.PATH}"
  }
  triggers { pollSCM('H/5 * * * *') }
  stages {
    stage('Checkout') { steps { git branch: 'main', url: 'https://github.com/bella06-09/8.2CDevSecOps.git' } }
    stage('Install Dependencies') { steps { sh 'npm install --no-audit --no-fund' } }
    stage('Run Tests') { steps { sh 'npm test || true' } }
    stage('Generate Coverage') { steps { sh 'npm run coverage || true' } }
    stage('Security Audit') { steps { sh 'npm audit || true' } }
  }
}
