pipeline {
  agent any
  stages {
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            container(name: 'go', shell: 'sh') {
              sh 'go test'
            }

          }
        }

        stage('Build') {
          steps {
            container(name: 'go', shell: 'sh') {
              sh 'go build -o compiled'
            }

          }
        }

      }
    }

    stage('asf') {
      steps {
        archiveArtifacts 'compiled'
      }
    }

  }
}