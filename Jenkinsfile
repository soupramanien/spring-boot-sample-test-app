pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build started'
        bat 'mvn -B -DskipTests clean package'
        echo 'Build finished'
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Unit tests starting'
            bat 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            echo 'Unit tests finished'
          }
        }

        stage('Integration') {
          steps {
            echo 'Integration tests starting'
            bat 'mvn -Dtest="com.example.testingweb.integration.**" test'
            echo 'Integration tests finished'
          }
        }

        stage('Functional') {
          steps {
            echo 'Functional tests starting'
            bat 'mvn -Dtest="com.example.testingweb.functional.**" test'
            echo 'Functional tests finished'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        echo 'Deployment is starting'
        bat 'mvn -B -DskipTests install'
        echo 'Deployment is finished'
      }
    }

  }
}