pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build and test') {
      steps {
        sh 'mvn clean test package'
      }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
      archiveArtifacts artifacts: 'target/*.war', allowEmptyArchive: true
    }
    success {
      echo 'ORS build succeeded'
    }
    failure {
      echo 'ORS build failed; inspect the console output and test report'
    }
  }
}