pipeline {
    agent none
    stages {
        stage('Build') {
            agent { label 'opensuse-sonar-docker' } 
            steps {
                checkout scm
                sh 'mvn clean install'
            }
            post {
                always {
                    junit '**/target/*.xml'
                }
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Windows": {
                        agent { label 'windows' } 
                        steps {
                            checkout scm
                            sh 'mvn clean install'
                        }
                        post {
                            always {
                                junit '**/target/*.xml'
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
