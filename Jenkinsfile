node {
       docker.withServer("tcp://192.168.100.8:2375") { 
           
              docker.withRegistry('https://hub.carlspring.org'){
                     def centos = docker.image('jenkins/centos-slave');
                     stage('Pull') {
                            centos.pull()    
                     }
                     stage('Build') {
                            centos.withRun {
                                   git 'https://github.com/strongbox/strongbox.git'
                                   
                                   sh 'echo JAVA_HOME=${JAVA_HOME}'
                                   sh 'echo M2_HOME=${M2_HOME}'
                                   
                                   withMaven(maven: 'maven-3.3.9') {
                                          sh 'mvn clean install'
                                   }
                            }
                     }
              }

       }
}
