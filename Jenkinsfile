pipeline {
       agent { label 'master' }
       stages {
              stage('Build') {
                     steps {
                            sh "mvn clean install"
                     }
              }
       }
       post {
            always {
                junit '**/reports/**/*.xml'
            }
       }
}
