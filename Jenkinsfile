node {
       
    docker.withServer("tcp://192.168.100.8:2375") { 
        def maven = docker.image('maven:3.3.9-jdk-8');

        stage('Pull') {
            maven.pull()    
        }
        
        stage('Build') {
              withDockerContainer(image: 'maven:3.3.9-jdk-8', toolName: 'docker') {
                     git 'https://github.com/strongbox/strongbox.git'                    
                     sh 'mvn -B clean instll'
              }
        }
    }
}
