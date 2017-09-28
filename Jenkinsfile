pipeline {
  agent {
    node {
      label 'JAVA'
    }
    
  }
  stages {
    stage('prepare') {
      steps {
        tool(type: 'maven', name: 'Maven 3.3.9')
        tool(name: 'jdk8', type: 'jdk')
      }
    }
    stage('MVN-scribe-client') {
      steps {
        withMaven(jdk: 'jdk8', maven: 'Maven3') {
          sh 'mvn -B clean install -f scribe-client/pom.xml -DautoUpdate=false -DdataDirectory=/opt/dukascopy/jenkins/owasp-data/'
        }
        
      }
    }
    stage('MVN-scribe-log4j') {
      steps {
        withMaven(jdk: 'jdk8', maven: 'Maven3') {
          sh 'mvn -B clean install -DautoUpdate=false -DdataDirectory=/opt/dukascopy/jenkins/owasp-data/ -f scribe-log4j/pom.xml'
        }
        
      }
    }
    stage('Artifacts') {
      steps {
        archiveArtifacts '**/*.jar'
      }
    }
  }
}