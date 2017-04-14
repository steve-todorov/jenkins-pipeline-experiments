pipeline {
  agent {
    node {
      label 'opensuse-sonar-docker'
    }
  }
  stages {
    stage('Build') {
      steps {
        echo 'Build commands.'
      }
    }
    stage('Build on other OS\'s') {
      steps {
        parallel(
          "Build on Debian": {
            node(label: 'debian-docker') {
                echo 'Build on debian-docker.'
            }
          },
          "Build on CentOS": {
            node(label: 'centos-docker') {
                echo 'Build on centos-docker.'
            }                       
          },
          "Build on Ubuntu": {
            node(label: 'ubuntu-docker') {
                echo 'Build on ubuntu-docker.'
            }
          },
          "Build on Windows": {
            node(label: 'ubuntu-docker') {
                bat 'echo "Building on Windows"' 
            }
          }
        )
      }
    }
    stage('Deploy to stage') {
      steps {
          echo 'Deploying to stage.'
      }
    }
    stage('Integration tests') {
      steps {
          echo 'Running integration tests.'
      }
    }
    stage('Deploy') {
      steps {
          echo 'Running deploying to production.'
      }
    }
  }
}
