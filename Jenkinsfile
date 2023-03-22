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
            echo 'debut: test d\'int�gration'
            bat 'mvnw -Dtest=com.example.testingweb.integration.** test'
            echo 'fin: test d\'int�gration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'd�but: test fonctionnel'
            bat 'mvnw -Dtest=com.example.testingweb.functional.** test'
            echo 'fin: test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'd�but: smoke test'
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