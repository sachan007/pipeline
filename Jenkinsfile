pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git credentialsId: '0e342ded-c462-4c28-bbd7-9c1f2bc9c966', url: 'git@github.com:sachan007/pipeline.git'
            }
        }
        stage('Code Stability') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
