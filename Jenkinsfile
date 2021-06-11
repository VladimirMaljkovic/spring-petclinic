pipeline {
  agent any
  stages {
    stage('pull sources') {
      parallel {
        stage('pull sources') {
          steps {
            git(url: 'https://github.com/VladimirMaljkovic/spring-petclinic', branch: 'main')
          }
        }

        stage('printing stuff') {
          steps {
            echo 'Pulling sources'
          }
        }

      }
    }

    stage('build') {
      parallel {
        stage('build') {
          steps {
            sh 'mvn install -DskipTests'
          }
        }

        stage('print') {
          steps {
            echo 'Building without tests...'
          }
        }

      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            sh 'mvn test'
          }
        }

        stage('print') {
          steps {
            echo 'testing'
          }
        }

      }
    }

    stage('publish') {
      steps {
        nexusArtifactUploader(nexusVersion: '3.30.1-01', nexusUrl: '172.16.238.7:8081', repository: 'maven-proxy-test')
      }
    }

  }
}