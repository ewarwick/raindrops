pipeline {
  agent any
  stages {
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            container(name: 'go', shell: 'sh') {
              sh 'go test ./cmd'
            }

          }
        }

        stage('Build') {
          steps {
            container(name: 'go', shell: 'sh') {
              sh 'go build -o compiled ./cmd'
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