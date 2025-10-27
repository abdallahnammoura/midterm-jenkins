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
          // you skipped tests, so don't fail when there are no reports
          junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
        }
      }
    }
    stage('Verify Artifact') { steps { sh 'ls -lh target/*.jar' } }
  }
}
