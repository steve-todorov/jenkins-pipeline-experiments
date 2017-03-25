pipeline {
    agent master
    tools { 
        maven 'maven-docker-3.3.9' 
        jdk 'jdk-1.8.0_65' 
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
        }
    }
}
