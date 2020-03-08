pipeline{
    agent any
    tools {
        go '1.14'
    }
    stages {
    
        stage("Test"){
            steps{
               echo "Start testing"
               echo "$PATH"
               sh 'cd app && go test -v 2>&1 | go-junit-report > report.xml'
            }
        }
    }
    post {
        always{
            junit "app/report.xml"
        }
    }
}