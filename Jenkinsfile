pipeline {
       agent { label 'opensuse-slave' }
       stages {
              stage('Build') {
                     steps {
                            sh "mvn clean install"
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
                junit(testResults: 'target/surefire-reports/**/*.xml')
                //archive "target/**/*"
                //step([$class: 'JUnitResultArchiver', testResults: '**/reports/junit/*.xml', healthScaleFactor: 1.0])
            }
       }
}
