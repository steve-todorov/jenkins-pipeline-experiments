pipeline {
    agent none
    stages {
        stage('Build') {
            echo 'Building opensuse...'
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Debian": {
                        steps {
                            agent { label 'debian-docker' }
                            steps {
                                git url: 'https://github.com/strongbox/strongbox.git'
                                sh 'mvn clean install'
                            }
                            post {
                                always {
                                    junit '**/target/surefire-reports/*.xml'
                                }
                            }
                        }
                    }
                )
            }
        }
        stage('Deploy to stage') {
            steps {
                echo 'Deploying to stage.'
            }
        }
        stage('Integration tests') {
            steps {
                echo 'Running integration tests.'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Running deploying to production.'
            }
        }
    }
}
