pipeline {
  agent any
  tools{
    nodejs 'nodejs-24-7-0'
  }
  stages {
    parallel {
      stage ('install depenedencies') {
        steps{
          sh 'npm install --no-audit'
        }
      }
      stage ('dependencies checking stage') {
            stage ('dependencies audit') {
              steps {
              sh 'npm audit --audit-level=critical'
              }
            }
            stage ('owasp dependency check') {
              steps {
                dependencyCheck additionalArguments: '''
                  --scan "./" \
                  --out "./" \
                  --format "ALL" \
                  --prettyPrint
                ''',
                odcInstallation: 'dependency-check-12.1.7'
              }
            }
      }
    }
  }
}
