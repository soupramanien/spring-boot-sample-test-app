pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va dÃ©marrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction terminée'
      }
    }

    stage('Test') {
      steps {
        echo 'Test unitaire va d�marrer'
        sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
        echo 'test unitaire termin�'
      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
}