pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va dÃƒÆ’Ã†â€™Ãƒâ€šÃ‚Â©marrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction terminÃƒÆ’Ã‚Â©e'
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Test unitaire va dÃƒÂ©marrer'
            sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            echo 'test unitaire terminÃƒÂ©'
          }
        }

        stage('Integration') {
          steps {
            echo 'est d\'integration va dÃ©marrer'
            sh 'mvn -Dtest="com.example.testingweb.integration.**" test'
            echo 'test d\'integration terminÃ©'
          }
        }

        stage('Functional') {
          steps {
            echo 'test fonctionnel va demarrer'
            sh 'mvn -Dtest="com.example.testingweb.functional.**" test'
            echo 'test fonctionnel terminé'
          }
        }

      }
    }

    stage('Deploy') {
      steps {
        echo 'd�ploiement va d�marrer'
        sh 'mvn -DskipTests install'
        echo 'd�ploiement termin�'
      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
}