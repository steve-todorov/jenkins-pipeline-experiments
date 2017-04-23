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

    stage('Build') {
        docker.image('maven:3.3.3-jdk-8').inside {
            sh 'mvn clean install'
        }
    }

}
