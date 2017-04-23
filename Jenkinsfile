// if(Jenkins.instance.getNode('windows').toComputer().isOffline()) {
//     echo "Will skip triggering build on Windows node because it's ofline."
// } else {
//     map["Build on Windows"] = {
//         node('windows') {
//             echo 'Building on Windows!'
//         }
//     }
// }


node {
    docker.withServer("tcp://jenkins-experimental.carlspring.org:2375") { 
        docker.image('maven:3.3.3-jdk-8').pull()
        docker.image('maven:3.3.3-jdk-8').inside {
            sh 'mvn clean install'
        }
    }
}
