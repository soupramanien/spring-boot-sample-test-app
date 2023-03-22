pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'début de l\'étape Build'
        bat ' mvnw -DskipTests clean install'
        echo 'fin de Build'
      }
    }

    stage('test') {
      parallel {
        stage('test intÃ©gration') {
          steps {
            echo 'test d\'intÃ©gration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'smoke test'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        echo 'stage deploy'
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}