pipeline {
  agent { 
    docker { 
      image 'mcr.microsoft.com/playwright:v1.23.0-focal'
    } 
  }
  stages {
    stage('install playwright') {
      steps {
        sh '''
          npm i -D @playwright/test
          npx playwright install
        '''
      }
    }
    stage('run help command') {
      steps {
        sh 'npx playwright test --help'
      }
    }
    stage('Run tests') {
      steps {
        sh '''
          npx playwright test --list
          npx playwright test
        '''
      }
      post {
        success {
          archiveArtifacts(artifacts: 'homepage-*.png', followSymlinks: false)
          sh 'rm -rf *.png'
        }
      }
    }
  }
}