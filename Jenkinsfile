def parallelSteps = [:]

map["Build on Debian"] = {
    node(label: 'debian-docker') {
        echo 'Build on debian-docker.'
    }
}
map["Build on CentOS"] = {
    node(label: 'centos-docker') {
        echo 'Build on centos-docker.'
    }
}
map["Build on Ubuntu"] = {
    node(label: 'ubuntu-docker') {
        echo 'Build on ubuntu-docker.'
    }
}


//    "Build on Windows": {
//        node(label: 'windows') {
//            bat 'echo "Building on Windows"'
//        }
//    }


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
            agent { label 'master' }
            steps {
                echo 'Build on master'
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(parallelSteps)
            }
        }
    }
}
