pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git credentialsId: '0e342ded-c462-4c28-bbd7-9c1f2bc9c966', url: 'git@github.com:sachan007/private.git'
            }
        }
        stage('Email') {
            steps {
                mail bcc: '', body: 'Going to deploy', cc: '', from: '', replyTo: '', subject: 'to deploy', to: 'abhisheksachaneee@gmail.com'
            }
        }
        stage('Slack to deploy') {
            steps {
                slackSend iconEmoji: '', message: 'Going to deploy', tokenCredentialId: 'SlackOpstree', username: ''
            }
        }
         stage('User input to start deploy') {
            steps {
                input message: 'Please confirm to deploy', submitter: 'sachan007'
            }
        }
        stage('Code Stability') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/PublishPipeline2 && mvn compile'
            }
        }
        stage('Code Quality') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/PublishPipeline2 && mvn checkstyle:checkstyle'
            }
        }
        stage('Code Coverage') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/PublishPipeline2 && mvn cobertura:cobertura'
            }
        }
         stage('Publish Reports') {
            steps {
                findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '', unHealthy: ''
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: '80'
                publishCoverage adapters: [coberturaAdapter('target/site/cobertura/coverage.xml')], sourceFileResolver: sourceFiles('NEVER_STORE')
            }
        }
         stage('User input to deploy?') {
            steps {
                input message: 'Do you want to deploy?', submitter: 'sachan007'
            }
        }
         stage('Build') {
            steps {
                sh 'mvn install'
            }
        }
        stage('Deploy to tomcat') {
            steps {
                sh 'cp target/Spring3HibernateApp.war /var/www/html'
            }
        }
    }
}
