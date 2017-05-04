pipeline {
       agent { label 'opensuse-slave' }
       stages {
              stage('Build') {
                     steps {
                            sh "mvn clean install"
                     }
              }
       }
       post {
            always {
                junit 'target/surefire-reports/*.xml'
            }
       }
}
