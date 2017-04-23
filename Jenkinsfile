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
    
        def maven = docker.image('maven:3.3.9-jdk-8'); // https://registry.hub.docker.com/_/maven/

        stage('Pull') {
            maven.pull()    
        }
        
        stage('Build') {
            maven.inside {
                //sh 'mvn -B clean install'
                sh 'echo "Is this outputing?"'
            }


    //  docker.withRegistry('https://hub.carlspring.org', 'b13411b8-78e8-4f1d-bdbe-c5a0e043d661') {
    //      docker.image('hmaven:3.3.9-jdk-8').pull()
    //      docker.image('maven:3.3.9-jdk-8').inside() {
    //          git 'https://github.com/strongbox/strongbox.git'
    //          sh 'mvn clean install'
    //      }
    //  }
        }
    }
}
