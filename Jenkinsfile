pipeline {
  agent any
  options { timestamps() }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Build') {
      steps {
        sh 'chmod +x mvnw || true'
        sh './mvnw -B -DskipTests clean package'
      }
      post {
        success {
          archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
          junit 'target/surefire-reports/*.xml'
        }
      }
    }
    stage('Verify Artifact') { steps { sh 'ls -lh target/*.jar' } }
  }
}
