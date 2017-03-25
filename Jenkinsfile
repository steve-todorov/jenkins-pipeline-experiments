pipeline {
    agent any
    tools { 
        maven 'maven-3.3.9' 
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
