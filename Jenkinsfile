pipeline {
  agent {
    node {
      label 'mvn352'
    }

  }
  stages {
    stage('error') {
      steps {
        sh '''ls -al
pwd

mvn --version
'''
      }
    }
  }
}