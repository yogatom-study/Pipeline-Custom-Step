pipeline {
  agent none
  stages {
    stage('Maven Build') {
      parallel {
        stage('Build JDK 21') {
          agent {
            node {
              label 'jdk21'
            }
          }
          steps {
            sh './scripts/build.sh'
          }
          post {
            success {
              stash(name: 'Java 21', includes: 'target/**')
            }
          }
        }
        stage('Build JDK 17') {
          agent {
            node {
              label 'jdk17'
            }
          }
          steps {
            sh './scripts/build.sh'
          }
          post {
            success {
            archiveArtifacts 'target/*.jar'
            stash(name: 'Java 17', includes: 'target/**')
            }
          }
        }
      }
    }
  }
}
