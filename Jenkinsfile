node {
       docker.withServer("tcp://192.168.100.8:2375") { 
           
              docker.withRegistry('https://hub.carlspring.org'){
                     def centos = docker.image('jenkins/centos-slave');
                     stage('Pull') {
                            centos.pull()    
                     }
                     stage('Build') {
                            centos.withRun('-v /tmp/m2repo:~/.m2/repository') {
                                   git 'https://github.com/strongbox/strongbox.git'
                                   
                                   sh 'echo JAVA_HOME=${JAVA_HOME}'
                                   sh 'echo M2_HOME=${M2_HOME}'
                                   
                                   withMaven(maven: 'maven-3.3.9', 
                                             mavenSettingsConfig: '5559dcfd-49b3-4ef8-b6e6-1a9b690a9aa2',
                                             mavenLocalRepo: '.repository') 
                                   {
                                          sh 'mvn clean install'
                                   }
                            }
                     }
              }

       }
}
