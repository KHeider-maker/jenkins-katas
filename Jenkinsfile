pipeline {
  agent any
  stages {
    stage('Hello UKH') {
      parallel {
        stage('Hello UKH') {
          steps {
            sh 'echo "hello UKH"'
          }
        }

        stage('build app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

  }
}