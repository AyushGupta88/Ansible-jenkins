pipeline {
  agent any
  stages {
    stage('Checkout') {
      parallel {
        stage('Checkout') {
          steps {
            sh 'date'
          }
        }

        stage('') {
          steps {
            echo 'Hello'
          }
        }

      }
    }

    stage('Sleep') {
      steps {
        sleep 100
      }
    }

  }
}