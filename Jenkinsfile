pipeline {
  agent any
  tools{
    nodejs 'nodejs-24-7-0'
  }
  environment {
  MONGO_URI = "mongodb+srv://supercluster.d83jj.mongodb.net/superData"
  }
  stages {
      stage ('install depenedencies') {
        steps{
          sh 'npm install --no-audit'
        }
      }
      stage ('dependencies checking stage') {
        parallel {
            stage ('dependencies audit') {
              steps {
              sh 'npm audit --audit-level=critical'
              }
            }
            stage ('owasp dependency check') {
              steps {
                  dependencyCheck additionalArguments: ''' //small error
                    --scan "./" \
                    --out "./" \
                    --format "ALL" \
                    --prettyPrint
                  ''',
                  odcInstallation: 'dependency-check-12.1.7'
                  dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true
              }
            }
        }
      }
      stage ('nodejs testing') {
        steps{
          withCredentials([usernamePassword(credentialsId: 'mongo-db-credentials', passwordVariable: 'MONGO_PASSWORD', usernameVariable: 'MONGO_USERNAME')]) {
            sh 'npm test'
          }
        }
      }
  }
}
