pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build starting'
        echo 'Build finished'
        bat 'mvn -DskipTests clean package'
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Unit tests starting'
            echo 'Unit tests finished'
          }
        }

        stage('Integration') {
          steps {
            echo 'Integration tests starting'
            echo 'Integration tests finished'
          }
        }

      }
    }

  }
}