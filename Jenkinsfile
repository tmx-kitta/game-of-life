node {
  stage('build') {
    sh '/usr/share/java/maven-3/bin/mvn compile'
  }

  stage('test') {
    sh '/usr/share/java/maven-3/bin/mvn test'
    junit '**/target/surefire-reports/*.xml'
  }

  stage('integlation test') {
    parallel firefox: {
    sh '/usr/share/java/maven-3/bin/mvn clean verify -B -pl gameoflife-web -Dsurefire.useFile=false -Dwebdriver.driver=firefox -Dwebdriver.port=9092 -Djetty.stop.port=9997'
  }, htmlunit: {
      sh '/usr/share/java/maven-3/bin/mvn clean verify -B -pl gameoflife-web -Dsurefire.useFile=false -Dwebdriver.driver=htmlunit -Dwebdriver.port=9092 -Djetty.stop.port=9997'
   }
  }

  stage('install') {
      sh '/usr/share/java/maven-3/bin/mvn clean install -B -Dsurefire.useFile=false'
      archiveArtifacts '**/target/*.jar'
  }
}
