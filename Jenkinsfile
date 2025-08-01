pipeline {
  agent any

  stages {
    stage('Verify Java/Gradle') {
      steps {
        script {
          if (isUnix()) {
            sh 'java -version'
            sh './gradlew --version'
          } else {
            bat 'java -version'
            bat 'gradlew.bat --version'
          }
        }
      }
    }

    stage('Build & Test') {
      steps {
        script {
          if (isUnix()) {
            sh './gradlew clean build --no-daemon'
          } else {
            bat 'gradlew.bat clean build --no-daemon'
          }
        }
      }
    }

    stage('Publish Test Results') {
      steps {
        junit '**/build/test-results/test/*.xml'
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
      }
    }
  }

  post {
    success {
      echo 'Build succeeded'
    }
    failure {
      echo 'Build failed'
    }
  }
}
