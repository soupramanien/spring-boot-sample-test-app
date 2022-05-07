pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''mvn -B -DskipTests clean package
'''
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
          }
        }

        stage('Integration') {
          steps {
            sh 'mvn -Dtest="com.example.testingweb.integration.**" test'
          }
        }

        stage('Functional') {
          steps {
            sh '''mvn -Dtest="com.example.testingweb.functional.**" test
'''
          }
        }

      }
    }

    stage('Deploy') {
      steps {
        sh 'mvn install'
      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
}