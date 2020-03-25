pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        container(name: 'go', shell: 'bash') {
          sh 'go test'
        }

      }
    }

  }
}