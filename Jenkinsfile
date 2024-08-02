pipeline {
    agent any

    stages {
        stage('Pre-Build') {
            steps {
                sh 'cmake -DCMAKE_BUILD_TYPE=Debug .'
                sh 'make'
            }
        }
        stage('Build') {
            steps {
                sh 'make'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'make test'
            }
        }
        stage('Code Coverage') {
            steps {
                sh 'gcov main.cpp'
            }
        }
        stage('Static Analysis') {
            steps {
                sh 'sonar-scanner -Dsonar.projectKey=myproject -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000'
            }
        }
    }
    post {
        success {
            mail to: 'Veeramally.Supriya@ltts.com',
                 subject: 'Build Success',
                 body: 'Build logs attached',
                 attachments: 'build.log'
        }
        failure {
            mail to: 'Veeramally.Supriya@ltts.com',
                 subject: 'Build Failure',
                 body: 'Build logs attached',
                 attachments: 'build.log'
        }
    }
}
