pipeline {
  agent any
  stages {
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            container(name: 'go', shell: 'sh') {
              sh '''gotestsum --junitfile ./testresults/unit-tests.xml -- -coverprofile=c.out ./...
go tool cover -html=c.out -o ./testresults/coverage.html'''
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
        junit(testResults: 'testresults/*.xml', keepLongStdio: true)
        script {
          script {
            publishHTML(target: [
              allowMissing: false,
              alwaysLinkToLastBuild: false,
              keepAll: true,
              reportDir: 'testresults',
              reportFiles: '*.html',
              reportTitles: "SimpleCov Report",
              reportName: "SimpleCov Report"
            ])
          }
        }

      }
    }

  }
}