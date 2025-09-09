pipeline {
  agent any

  // Explicitly add Homebrew Node to PATH for Jenkins
  environment {
    NODE_HOME = "/opt/homebrew/opt/node@18"
    PATH = "${NODE_HOME}/bin:/opt/homebrew/bin:/usr/local/bin:${env.PATH}"
  }

  triggers { pollSCM('H/5 * * * *') }

  stages {
    stage('Verify Node') {
      steps {
        sh '''
          echo "whoami: $(whoami)"
          which node || true
          node -v || true
          which npm || true
          npm -v || true
        '''
      }
    }

    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/bella06-09/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps { sh 'npm install --no-audit --no-fund' }
    }

    stage('Run Tests') {
      steps { sh 'npm test || true' }
    }

    stage('Generate Coverage') {
      steps { sh 'npm run coverage || true' }
    }

    stage('Security Audit') {
      steps { sh 'npm audit || true' }
    }
  }
}
