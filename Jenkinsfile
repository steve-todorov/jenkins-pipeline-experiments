node {
       
    docker.withServer("tcp://192.168.100.8:2375") { 
    
        def maven = docker.image('maven:3.3.9-jdk-8');

        stage('Pull') {
            maven.pull()    
        }
        
        stage('Build') {
            maven.inside {
                stage("Container") {
                    git 'https://github.com/strongbox/strongbox.git'                    
                    sh 'echo "Is this outputing?"'
                }
            }
        }
    }
}
