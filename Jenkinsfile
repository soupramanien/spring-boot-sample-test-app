pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'dÃ©but de l\'Ã©tape Build'
        bat ' mvnw -DskipTests clean install'
        echo 'fin de Build'
      }
    }

    stage('test') {
      parallel {
        stage('test intÃƒÂ©gration') {
          steps {
            echo 'debut: test d\'intégration'
            bat 'mvnw -Dtest=com.example.testingweb.integration.** test'
            echo 'fin: test d\'intégration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'début: test fonctionnel'
            bat 'mvnw -Dtest=com.example.testingweb.functional.** test'
            echo 'fin: test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'début: smoke test'
            bat 'mvnw -Dtest=com.example.testingweb.smoke.** test'
            echo 'fin: smoke test'
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