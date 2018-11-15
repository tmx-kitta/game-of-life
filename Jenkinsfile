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
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            withMaven(maven: 'mvn3') {
              sh 'mvn clean install -B -Dsurefire.useFile=false'
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
    stage('Metrics') {
      steps {
        sh 'mvn clean verify site -Pmetrics -B -Dwebdriver.port=9093 -Djetty.stop.port=9996'
      }
    }
  }
  environment {
    JAVA_HOME = '/usr/local/jdk1.8.0_161'
  }
}