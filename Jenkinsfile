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
      steps {
        echo 'Test unitaire va démarrer'
        sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
        echo 'test unitaire terminé'
      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
}