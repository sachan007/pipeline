pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github', url: 'git@github.com:sachan007/OT-Java-WebApp.git''
            }
        }
        stage('Email') {
            steps {
                mail bcc: '', body: 'Going to deploy', cc: '', from: '', replyTo: '', subject: 'to deploy', to: 'abhisheksachaneee@gmail.com'
            }
        }
        stage('Slack to deploy') {
            steps {
                slackSend iconEmoji: '', message: 'Abhishek is Going to deploy', tokenCredentialId: 'SlackOpstree', username: ''
            }
        }
         stage('User input to start deploy') {
            steps {
                input message: 'Please confirm to deploy', submitter: 'sachan007'
            }
        }
        stage('Code Stability') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Code Quality') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('Code Coverage') {
            steps {
                sh 'mvn cobertura:cobertura'
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
                sh 'mvn package'
            }
        }
        stage('Deploy to tomcat') {
            steps {
                sh 'cp target/Spring3HibernateApp.war /var/www/html'
            }
        }
    }
}
        post{
            success {
             slackSend iconEmoji: '', message: 'Abhishek job pass', tokenCredentialId: 'SlackOpstree', username: ''
            }
            falure {
              slackSend iconEmoji: '', message: 'Abhishek job fail', tokenCredentialId: 'SlackOpstree', username: ''
            }
        }




