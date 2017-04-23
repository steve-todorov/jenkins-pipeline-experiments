pipeline {
       agent none
       stages {
              stage('Build') {
                     agent { label 'opensuse-experimental' }
                     steps {
                            sh "whoami"
                     }
              }
       }
}
