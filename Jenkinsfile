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
        docker.image('httpd').withRun('-p 10234:80') {c ->
            sh "curl -i http://${hostIp(c)}:10234/"
        }
    }
}
