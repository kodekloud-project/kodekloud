pipeline {
  agent any
  tools{
    nodejs 'nodejs-24-7-0'
  }
  stages {
    stage ('install depenedencies') {
      steps{
        sh 'npm install --no-audit'
      }
    }
    stage ('dependencies audit') {
      steps {
      sh 'npm audit --audit-level=critical'
      }
    }
  }
}
