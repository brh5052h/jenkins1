pipeline {
  agent any

  stages {
    stage('Checkout Code') {
      steps {
        git branch: 'main',
            url: 'https://github.com/brh5052h/jenkins1.git',
            credentialsId: '33'
      }
    }

    stage('Verify Node') {
      steps {
        sh 'node -v || (echo \"Node not found on PATH\"; exit 1)'
        sh 'npm -v || (echo \"npm not found on PATH\"; exit 1)'
      }
    }

    stage('Install Dependencies') {
      steps {
        echo 'Installing dependencies...'
        sh 'npm ci'
      }
    }

    stage('Build App') {
      steps {
        echo 'Building application...'
        sh 'npm run build || echo \"No build script, continuing\"'
      }
    }

    stage('Run App in Background') {
      steps {
        echo 'Starting Node.js app in background...'
        sh '''
          nohup node server.js > app.log 2>&1 & sleep 2
          ps aux | grep node | grep -v grep || true
          tail -n 20 app.log || true
        '''
      }
    }
  }

  post {
    success {
      echo '✅ Build & Deployment Successful!'
      echo '🌐 Access your app at: http://13.53.103.201:3000/'
    }
    failure {
      echo '❌ Build failed. Check console logs for errors.'
    }
  }
}
