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
    stage('error') {
      steps {
        withMaven(maven: 'mvn3') {
          sh 'mvn clean install'
        }

      }
    }
  }
  environment {
    JAVA_HOME = '/usr/local/jdk1.8.0_161'
  }
}