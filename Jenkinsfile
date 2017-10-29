pipeline {
    agent {
        docker {
            args '-v /mnt/ramdisk/10:/home/jenkins --cap-add SYS_ADMIN'
            image 'hub.carlspring.org/jenkins/opensuse-slave:latest'
        }
    }
    options {
        timeout(time: 2, unit: 'HOURS')
        disableConcurrentBuilds()
        skipDefaultCheckout()
    }
    stages {
        stage('Setup workspace')
        {
            steps {
                script {
                    env.HDDWS=env.WORKSPACE
                    env.RAMWS="/home/jenkins/workspace/"+ sh(returnStdout: true, script: 'basename "${HDDWS}"').trim()
                    env.RAMMOUNT=env.WORKSPACE+"/ram"

                    cleanWs deleteDirs: true
                    checkout scm

                    echo "Preparing workspace..."
                    sh "mkdir -p '$RAMWS'"
                    sh "cp -R `ls -A '$HDDWS' | grep -v ram` '$RAMWS'"
                    sh "mkdir -p '$RAMMOUNT'"
                    sh "sudo mount --bind  '$RAMWS' '$RAMMOUNT'"
                }
            }
        }
        stage('Building...')
        {
            steps {
                withMaven(maven: 'maven-3.3.9', mavenSettingsConfig: 'a5452263-40e5-4d71-a5aa-4fc94a0e6833')
                {
                    sh "cd '$RAMMOUNT' && mvn -U clean install -Dmaven.test.failure.ignore=true"
                }
            }
        }
    }
    post {
        always {
            script {
                // unmount and copy back to hdd
                sh "sudo umount --force $RAMMOUNT"
                sh "cp -R '$RAMWS/.' '$RAMMOUNT'"
            }

            // remove unnecessary directories.
            sh "(cd '$HDDWS' && find . -maxdepth 1 ! -name 'ram' ! -name '.' ! -name '..' -exec rm -rf '{}' \\;)"

            // clean up ram
            sh "rm -rf '$RAMWS'"

            // (fallback) record test results even if withMaven should have done that already.
            junit '**/target/surefire-reports/*.xml'
            
            // Email notification
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: emailextrecipients([[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider'], [$class: 'FailingTestSuspectsRecipientProvider'], [$class: 'FirstFailingBuildSuspectsRecipientProvider']]),
                sendToIndividuals: true])
        }
    }
}
