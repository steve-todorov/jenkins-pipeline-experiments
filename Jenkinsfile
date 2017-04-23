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
    git 'https://github.com/strongbox/strongbox.git'
    docker.withServer("tcp://192.168.100.8:2375") { 
        docker.withRegistry('https://hub.carlspring.org', 'b13411b8-78e8-4f1d-bdbe-c5a0e043d661') {
            docker.image('jenkins/opensuse-sonar').inside() {
                withMaven(
                    mavenSettingsConfig: '5559dcfd-49b3-4ef8-b6e6-1a9b690a9aa2',
                    mavenLocalRepo: '.repository'
                ) 
                {
                    sh 'mvn clean install'
                }
            }
        }
    }
}
