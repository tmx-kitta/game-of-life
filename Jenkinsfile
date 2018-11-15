pipeline {
  agent {
    node {
      label 'mvn352'
    }

  }
  stages {
    stage('Smoke') {
      steps {
        sh '''mvn --version
java --version
'''
      }
    }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            withMaven(maven: 'mvn3') {
              sh 'mvn clean install -B -Dsurefire.useFile=false'
              sh 'mvn clean verify site -Pmetrics -B -Dwebdriver.port=9093 -Djetty.stop.port=9996'
            }

          }
        }
        stage('integration-tests') {
          steps {
            sh 'mvn clean verify -B -pl gameoflife-web -Dsurefire.useFile=false -Dwebdriver.driver=firefox -Dwebdriver.port=9092 -Djetty.stop.port=9997'
          }
        }
      }
    }
  }
  environment {
    JAVA_HOME = '/usr/local/jdk1.8.0_161'
  }
}