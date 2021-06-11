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

    stage ('Build & test') {
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

    stage('Send email') {
      def mailRecipients = "your_recipients@company.com"
      def jobName = currentBuild.fullDisplayName

      emailext body: '''${SCRIPT, template="groovy-html.template"}''',
        mimeType: 'text/html',
        subject: "[Jenkins] ${jobName}",
        to: "${mailRecipients}",
        replyTo: "${mailRecipients}",
        recipientProviders: [[$class: 'CulpritsRecipientProvider']]
}

  }
}