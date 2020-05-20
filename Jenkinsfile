pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
      }
    }

    stage('build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
      }
    }

    stage('test report') {
      parallel {
        stage('test report') {
          steps {
            junit '**/target/surefire-reports/TEST-*.xml'
          }
        }

        stage('archive file') {
          steps {
            archiveArtifacts 'target/*.jar'
          }
        }

      }
    }

    stage('print message') {
      steps {
        echo 'Build Finished~~~~~~~~~'
      }
    }

  }
}