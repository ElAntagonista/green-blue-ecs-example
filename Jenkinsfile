pipeline {
    agent any
    tools {
        go '1.14'
    }
    stages {
        stage("Checkout"){
            steps{
                git branch: 'master', url: 'https://github.com/ElAntagonista/green-blue-ecs-example.git'
            }
        }
        stage("Test"){
            steps{
               echo "Start testing"
               echo "$PATH"
               sh 'cd app && go test -v 2>&1 | go-junit-report > report.xml'
            }
        }
        stage("Build"){
            steps{
                echo "Starting build process"
                sh 'cd app && go build'
            }
        }
        Trigger job
        Evaluate condition on
        stage("Trigger Another Pipeline"){
            when { expression { return true} }   
            steps {
                build job: 'Progress/BuildGo'
             }
        }
    }
    post {
        always{
            junit "app/report.xml"
            cleanWs()
            logstash
        }
    }
}
