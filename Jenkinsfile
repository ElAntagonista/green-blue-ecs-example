pipeline{
    agent any
    tools {
        go 'Go 1.13'
    }
    stages {
        stage("Preparation"){
            steps{
                echo "Installing supporting toolset"
                sh "go get -u github.com/jstemmer/go-junit-report"
            }
        }
        stage("Test"){
            steps{
               echo "Start testing"
               sh "cd app"
               sh "go test -v 2>&1 | go-junit-report > report.xml"
            }
        }
    }
    post {
        always{
            junit "app/report.xml"
        }
    }
}