pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va dÃƒÆ’Ã‚Â©marrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction terminÃƒÂ©e'
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Test unitaire va dÃ©marrer'
            sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            echo 'test unitaire terminÃ©'
          }
        }

        stage('Integration') {
          steps {
            echo 'est d\'integration va démarrer'
            sh 'mvn -Dtest="com.example.testingweb.integration.**" test'
            echo 'test d\'integration terminé'
          }
        }

        stage('Functional') {
          steps {
            echo 'test fonctionnel va demarrer'
            sh 'mvn -Dtest="com.example.testingweb.functional.**" test'
            echo 'test fonctionnel termin�'
          }
        }

      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
}