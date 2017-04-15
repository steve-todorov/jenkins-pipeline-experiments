// if(Jenkins.instance.getNode('windows').toComputer().isOffline()) {
//     echo "Will skip triggering build on Windows node because it's ofline."
// } else {
//     map["Build on Windows"] = {
//         node('windows') {
//             echo 'Building on Windows!'
//         }
//     }
// }

pipeline {
    agent none
    stages {
        stage('Build') {
            agent { label 'opensuse-sonar-docker' }
            steps {
                git url: 'https://github.com/strongbox/strongbox.git'
                sh 'mvn clean install'
                junit '**/target/*.xml'
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Debian": {
                        node(label: 'debian-docker') {
                            git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
                            junit '**/target/*.xml'
                        }
                    },
                    "Build on CentOS": {
                        node(label: 'centos-docker') {
                            git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
                            junit '**/target/*.xml'
                        }
                    },
                    "Build on Ubuntu": {
                        node(label: 'ubuntu-docker') {
                            git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
                            junit '**/target/*.xml'
                        }
                    },
                    "Build on Windows": {
                        node(label: 'windows') {
                            git url: 'https://github.com/strongbox/strongbox.git'
                            bat 'mvn clean install'
                            junit '**/target/*.xml'
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
