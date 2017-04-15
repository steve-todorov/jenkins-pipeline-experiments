pipeline {
    agent { label 'opensuse-sonar-docker' }
    stages {
        stage('Build') {
            steps {
                checkout scm
                try {
                    sh 'mvn clean install'
                }
                finally {
                    junit '**/target/*.xml'
                }
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Debian": {
                        agent { label 'debian-docker'}
                        steps {
                            checkout scm
                            try {
                                sh 'mvn clean install'
                            }
                            finally {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on CentOS": {
                        node(label: 'centos-docker') {
                            checkout scm
                            try {
                                sh 'mvn clean install'
                            }
                            finally {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on Ubuntu": {
                        node(label: 'ubuntu-docker') {
                            checkout scm
                            try {
                                sh 'mvn clean install'
                            }
                            finally {
                                junit '**/target/*.xml'
                            }
                        }
                    },
                    "Build on Windows": {
                        node(label: 'windows') {
                            checkout scm
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
