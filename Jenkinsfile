pipeline {
  agent any

  stages {
    stage('Verify Java/Gradle') {
      steps {
        sh 'java -version'
        sh './gradlew --version'
      }
    }

    stage('Build & Test') {
      steps {
        sh './gradlew clean build --no-daemon'
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
    success { echo 'Build succeeded' }
    failure { echo 'Build failed' }
  }
}
