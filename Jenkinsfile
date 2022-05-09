pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build starting'
        bat 'mvn -DskipTests clean package'
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
            echo 'Integration tests finished'
          }
        }

        stage('Functional') {
          steps {
            echo 'Functional tests starting'
            echo 'Functional tests finished'
          }
        }

      }
    }

    stage('Deploy') {
      steps {
        echo 'Deployment starting'
        echo 'Deployment finished'
      }
    }

  }
}