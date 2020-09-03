pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/jebrze/devops-webapp1', branch: 'master')
      }
    }

    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''whoami
date
echo $PATH
pwd
ls -la
./gradlew build --info'''
          }
        }

        stage('P1') {
          steps {
            sh 'echo run parallel'
          }
        }

      }
    }

    stage('Publish') {
      parallel {
        stage('Publish') {
          steps {
            archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
          }
        }

        stage('Publish2') {
          steps {
            sh 'echo publishing in parallel'
          }
        }

      }
    }

  }
}