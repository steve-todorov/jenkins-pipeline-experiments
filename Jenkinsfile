pipeline {
       agent { label 'opensuse-slave' }
       stages {
              stage('Build') {
                     steps {
                            sh "mvn clean install -Dmaven.test.failure.ignore=true"
                     }
              }
              stage('Finish') {
                    steps {
                           echo "Done."
                    }
              }
       }
       post {
            always {
                archive "target/**/*"
                junit "**/surefire-reports/*.xml"
                //step([$class: 'JUnitResultArchiver', testResults: '**/reports/junit/*.xml', healthScaleFactor: 1.0])
            }
       }
}
