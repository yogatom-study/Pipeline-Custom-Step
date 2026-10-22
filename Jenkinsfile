@Library('shared-library') _

pipeline {
    agent none

    stages {
        stage('Maven Build') {
            parallel {
                stage('Build JDK 21') {
                    agent { label 'tom-cloud' }
                    steps {
                        sh './jenkins/build.sh'
                    }
                    post {
                        success {
                            stash(name: 'Java 21', includes: 'target/**')
                        }
                    }
                }

                stage('Build JDK 17') {
                    agent { label 'tom-cloud' }
                    steps {
                        sh './jenkins/build.sh'
                    }
                    post {
                        success {
                            postBuildSuccess(stashName: "Java 17")
                        }
                    }
                }
            }
        }
    }
}
