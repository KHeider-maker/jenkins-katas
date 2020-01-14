pipeline {
  agent any
  stages {
    stage('Clone down') {
      steps {
        sh 'echo "hello clone down"'
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