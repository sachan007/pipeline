pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git credentialsId: '0e342ded-c462-4c28-bbd7-9c1f2bc9c966', url: 'git@github.com:sachan007/private.git'
            }
        }
        stage('Code Stability') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/PublishPipeline && mvn compile'
            }
        }
                stage('User input') {
            steps {
                input 'Do you want to proceed with further steps?'
            }
        }
                stage('Build') {
            steps {
                sh 'mvn install'
            }
        }
    }
}
