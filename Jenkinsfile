def parallelSteps = [:]

if(Jenkins.instance.getNode('windows').toComputer().isOffline()) {
    echo "Will skip triggering build on Windows node because it's ofline."
} else {
    parallelSteps["Build on Windows"] = {
        echo 'Building on Windows!'
    }
}

parallelSteps["Build on Debian"] = {
    node('debian') {
        echo "Building on Debian"
    }
}

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
                parallel(parallelSteps)
            }
            post {
                always {
                    echo 'This will always run'
                }
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
