pipeline {
  agent any
  tools {
        maven 'maven'
        jdk 'jdk8'
  }
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

    stage ('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
                echo 'starting junit step rn'
            }
            
            post {
                success {
                    sh 'mvn test'
                    junit 'target/surefire-reports/**/*.xml' 
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