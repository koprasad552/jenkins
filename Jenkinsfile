pipeline {
    agent {
        label 'k8s-agent-second'
    }
    stages {
        stage('Run maven') {
        steps {
            container('maven') {
            sh 'mvn -version'
                }
            container('busybox') {
            sh '/bin/busybox'
                }
            }
        }
    }
}