pipeline {
    agent { label 'opensuse-sonar-docker' }
    stages {
        stage('Build') {
            agent { label 'opensuse-sonar-docker' }
            steps {
                git url: 'https://github.com/strongbox/strongbox.git'
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
                    "Build on Debian": {
                        agent { label 'debian-docker' }
                        steps {
			                git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
                        }
                        post {
                            always {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on CentOS": {
                        agent { label 'centos-docker' }
                        steps {
			                git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
                        }
                        post {
                            always {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on Ubuntu": {
                        agent { label 'ubuntu-docker' }
                        steps {
			                git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
                        }
                        post {
                            always {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on Windows": {
                        agent { label 'windows' }
                        steps {
			                git url: 'https://github.com/strongbox/strongbox.git'
                            bat 'mvn clean install'
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
