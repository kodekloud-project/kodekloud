pipeline {
  agent any
  tools{
    nodejs 'nodejs-24-7-0'
  }
  stages {
    stage ('nodejs check') {
      steps{
        sh '''
            node -v
            npm -v
        '''
      }
    }
  }
}
