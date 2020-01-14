pipeline {
  agent any
  stages {
    stage('Clone down') {
      agent {
        label 'host'
      }
      steps {
        sh 'echo "hello clone down"'
        stash 'code'
      }
    }

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
          options {
            skipDefaultCheckout(true)
          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            deleteDir()
          }
        }

      }
    }

  }
}