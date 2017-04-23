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
                     withMaven(jdk: 'openjdk-1.8.0_121', maven: 'maven-3.3.9', mavenSettingsConfig: '5559dcfd-49b3-4ef8-b6e6-1a9b690a9aa2') {
                         sh 'mvn -B clean instll'
                     }                
                }
            }
        }
    }
}
