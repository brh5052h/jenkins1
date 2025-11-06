
pipeline {
    agent any

    tools {
        nodejs 'node23'  // use your NodeJS tool name from Jenkins Global Tool Config
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/brh5052h/jenkins1.git',
                    credentialsId: '33'
            }
        }

       stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies...'
                sh 'npm install'
            }
        }

        stage('Build App') {
            steps {
                echo 'Building application...'
                sh 'echo Build successful'
            }
        }

        stage('Run App in Background') {
  steps {
    echo 'Starting Node.js app in background...'
    sh '''
      nohup node server.js > app.log 2>&1 &
      sleep 2
      ps aux | grep node | grep -v grep
      tail -n 10 app.log || true
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
