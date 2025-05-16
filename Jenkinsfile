pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Anushi-Amarasinghe/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true' 
      }
      post {
        always {
          emailext (
            subject: "Tests Stage: ${currentBuild.currentResult} - ${env.JOB_NAME}",
            body: """
              Tests stage completed with status: ${currentBuild.currentResult}.
              Build URL: ${env.BUILD_URL}
              Logs are attached.
            """,
            to: 'pereraanu804@gmail.com', // Replace with your email
            attachmentsPattern: '**/logs/*.log', // Attach specific logs if needed
            attachLog: true // Attach the full build log
          )
        }
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
      post {
        always {
          emailext (
            subject: "Security Scan: ${currentBuild.currentResult} - ${env.JOB_NAME}",
            body: """
              Security scan completed with status: ${currentBuild.currentResult}.
              Build URL: ${env.BUILD_URL}
              Logs are attached.
            """,
            to: pereraanu804@gmail.com', // Replace with your email
            attachLog: true
          )
        }
      }
    }
  }

  post {
    always {
      emailext (
        subject: "Final Build Status: ${currentBuild.currentResult} - ${env.JOB_NAME}",
        body: """
          Pipeline completed with status: ${currentBuild.currentResult}.
          Build URL: ${env.BUILD_URL}
          Full logs are attached.
        """,
        to: 'pereraanu804@gmail.com',
        attachLog: true
      )
    }
  }
}
