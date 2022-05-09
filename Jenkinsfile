pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va dÃƒÂ©marrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction terminÃ©e'
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Test unitaire va démarrer'
            sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            echo 'test unitaire terminé'
          }
        }

        stage('Integration') {
          steps {
            echo 'est d\'integration va d�marrer'
            sh 'mvn -Dtest="com.example.testingweb.integration.**" test'
            echo 'test d\'integration termin�'
          }
        }

      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
}