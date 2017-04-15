pipeline {
    agent {
        node {
            label 'opensuse-sonar-docker'
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build commands.'
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Debian": {
                        agent { label: 'debian-docker' }
                        steps {
                            echo 'Build on debian-docker.'
                        }
                        post {
                            always {
                                echo 'Post Debian'
                            }
                        }
                    },
                    "Build on CentOS": {
                        agent { label: 'centos-docker' }
                        steps {
                            echo 'Build on centos-docker.'
                        }
                        post {
                            always {
                                echo 'Post CentOS'
                            }
                        }
                    },
                    "Build on Ubuntu": {
                        agent { label: 'ubuntu-docker' }
                        steps {
                            echo 'Build on ubuntu-docker.'
                        }
                        post {
                            always {
                                echo 'Post Ubuntu'
                            }
                        }
                    },
                    "Build on Windows": {
                        agent { label: 'windows' }
                        steps {
                            bat 'echo "Building on Windows"'
                        }
                        post {
                            always {
                                echo 'Post Windows'
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
