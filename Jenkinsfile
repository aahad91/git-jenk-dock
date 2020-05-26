pipeline {
  agent { docker { image 'python:3.7.2' } }
  stages {
    stage('test') {
      steps {
        sh 'python pipeline-test/test.py'
      }
    }
  }
}
