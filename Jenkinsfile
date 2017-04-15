pipeline {
    agent none
    stages {
        stage('Build') {
            agent { label 'master' }
            steps {
                echo 'Build on master'
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Windows": {
                        agent { label 'windows' }

                        // Conditional execution of this stage - only run this stage if the when condition is true.
                        when {
                            // One and only one condition is allowed.
                            // Only run if this Scripted Pipeline expression doesn't return false or null
                            expression {
                                return Jenkins.instance.getNode('windows').toComputer().isOnline()
                            }
                        }

                        steps {
                            git url: 'https://github.com/strongbox/strongbox.git'
                            sh 'mvn clean install'
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
