pipeline {
    agent { 
        label 'k8s-agent-second'
        }

    stages {
        stage('Get a Maven project') {
        git 'https://github.com/jenkinsci/kubernetes-plugin.git'
        container('maven') {
            stage('Build a Maven project') {
                sh 'mvn -B -ntp clean install'
            }
        }
    }
        stage('Get a Golang project') {
        git url: 'https://github.com/hashicorp/terraform-provider-google.git', branch: 'main'
        container('golang') {
            stage('Build a Go project') {
            sh '''
                mkdir -p /go/src/github.com/hashicorp
                ln -s `pwd` /go/src/github.com/hashicorp/terraform
                cd /go/src/github.com/hashicorp/terraform && make
            '''
            }
          }
        }
    }
}
