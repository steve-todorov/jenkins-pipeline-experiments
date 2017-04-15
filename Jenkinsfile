import jenkins.model.*

def parallelSteps = [:]

parallelSteps["Build on Debian"] = {
    node('debian') {
        echo "Building on Debian"
    }
}

//if(Jenkins.instance.getNode('windows').toComputer().isOffline()) {
//    echo "Will skip triggering build on Windows node because it's ofline."
//} else {
//    parallelSteps["Build on Windows"] = {
//        echo 'Building on Windows!'
//    }
//}

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
                parallel parallelSteps
            }
            post {
                always {
                    echo 'This will always run'
                }
            }
        }
    }
}
