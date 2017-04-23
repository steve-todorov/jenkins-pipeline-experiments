// if(Jenkins.instance.getNode('windows').toComputer().isOffline()) {
//     echo "Will skip triggering build on Windows node because it's ofline."
// } else {
//     map["Build on Windows"] = {
//         node('windows') {
//             echo 'Building on Windows!'
//         }
//     }
// }

docker.withDockerServer("tcp://jenkins-experimental.carlspring.org:2375") { 

    pipeline {
        agent none
        stages {
            stage('Build') {
                steps {
                    script {
                        def maven = docker.image('maven:3.3.3-jdk-8');
                        maven.pull()
                        maven.inside {
                            sh 'mvn clean install'
                        }
                    }
                }
            }
        }

    }

}
