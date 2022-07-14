pipeline {
    agent any
    options{
        disableConcurrentBuilds()
    }
    tools {
        git 'Default'
        maven "Maven 3.8.6"
    }
    stages {
        stage('build') {
            steps {
                sh '''
                mvn --version
                javac -version
                '''
            }
        }
        stage('clean') {
            steps {
               deleteDir()
            }
        }
        stage('zip') {
            steps {
                sh '''
                touch test.txt
                '''
               zip dir: '', exclude: '', glob: '', zipFile: 'test.zip'
            }
        }
        stage('clone') {
            steps {
                script{
                        checkout([$class: 'GitSCM', branches: [[name: '*/$BRANCH']], extensions: [], userRemoteConfigs: [[credentialsId: '$GITCRED', url: '$URL']]])

                }

            }
        }
    }
}
