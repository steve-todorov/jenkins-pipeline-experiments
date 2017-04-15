pipeline {
    agent { label 'opensuse-sonar-docker' }
    stages {
        stage('Build') {
            steps {
                node('opensuse-sonar-docker') {
                    ; checkout scm
		            git url: 'https://github.com/strongbox/strongbox.git'
		            
                    try {
                        sh 'mvn clean install'
                    }
                    finally {
                        junit '**/target/*.xml'
                    }
                }
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Debian": {
                        node('debian-docker') {
			                git url: 'https://github.com/strongbox/strongbox.git'

                            try {
                                sh 'mvn clean install'
                            }
                            finally {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on CentOS": {
                        node('centos-docker') {
			                git url: 'https://github.com/strongbox/strongbox.git'

                            try {
                                sh 'mvn clean install'
                            }
                            finally {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on Ubuntu": {
                        node('ubuntu-docker') {
			                git url: 'https://github.com/strongbox/strongbox.git'

                            try {
                                sh 'mvn clean install'
                            }
                            finally {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on Windows": {
                        node('windows') {
			                git url: 'https://github.com/strongbox/strongbox.git'

                            try {
                                bat 'mvn clean install'
                            }
                            finally {
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
