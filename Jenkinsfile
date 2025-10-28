pipeline {
  agent any

  environment {
    BRANCH_NAME = 'feature/login'
  }

  stages {
    stage('Checkout') {
      steps {
        echo "Checking out branch: ${env.BRANCH_NAME}"
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Building the login feature...'
        sh './gradlew build' // or your build tool
      }
    }

    stage('Unit Tests') {
      steps {
        echo 'Running unit tests...'
        sh './gradlew test'
      }
    }

    stage('Code Quality') {
      steps {
        echo 'Running static analysis...'
        sh './gradlew checkstyle' // or use SonarQube, ESLint, etc.
      }
    }

    stage('Archive Artifacts') {
      steps {
        archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
      }
    }
  }

  post {
    always {
      echo 'Cleaning up...'
      cleanWs()
    }
    success {
      echo 'Build succeeded!'
    }
    failure {
      echo 'Build failed.'
    }
  }
}
