pipeline {
  agent {
    node {
      label 'mvn352'
    }

  }
  stages {
    stage('Smoke') {
      steps {
        sh '''ls -al
pwd

mvn --version
'''
      }
    }
    stage('') {
      steps {
        withMaven(maven: 'mvn3') {
          sh 'mvn clean install'
        }

      }
    }
  }
}