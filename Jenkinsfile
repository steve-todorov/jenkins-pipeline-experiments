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
                archive "target/**/*"
                junit "target/surefire-reports/*.xml"
            }
       }
}
