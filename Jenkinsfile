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
            sh 'ci/unit-test-app.sh'
          }
        }

      }
    }

    stage('error') {
      environment {
        DOCKERCREDS = credentials('docker_login')
      }
      steps {
        sh '''unstash \'code\' //unstash the repository code
      sh \'ci/build-docker\'
      sh \'echo "$DOCKERCREDS_PSW" | docker login -u "$DOCKERCREDS_USR" --password-stdin\' //login to docker hub with the credentials above
      sh \'ci/push-docker.sh\''''
      }
    }

  }
}