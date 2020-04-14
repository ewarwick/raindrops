
  podTemplate(containers:[containerTemplate(name:'go', image:'golang:latest',ttyEnabled: true, command: 'cat')]) {

node(POD_LABEL){

      parallel (
        'test': {
            container(name: 'go', shell: 'sh') {
              sh '''mkdir testresults
go get gotest.tools/gotestsum
gotestsum --junitfile ./testresults/unit-tests.xml -- -coverprofile=c.out ./...
go tool cover -html=c.out -o ./testresults/coverage.html'''
            }

        },

        'Build': {
            container(name: 'go', shell: 'sh') {
              sh 'go build -o compiled ./cmd'
            }

        }

    )

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
