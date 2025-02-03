pipeline {
    agent { 
        label 'k8s-agent-second'
    }

    stages {
        stage('Get a Golang project') {
            steps {
                git(url: 'https://github.com/hashicorp/terraform-provider-google.git', branch: 'main')
                container('golang') {
                    sh '''
                        mkdir -p /go/src/github.com/hashicorp
                        ln -s `pwd` /go/src/github.com/hashicorp/terraform
                        cd /go/src/github.com/hashicorp/terraform && make
                    '''
                }
            }
        }
        stage('Get a Maven project') {
            steps {
                git 'https://github.com/jenkinsci/kubernetes-plugin.git'
                container('maven') {
                    sh 'mvn -B -ntp clean install'
                }
            }
        }
    }
}
