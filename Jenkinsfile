pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va démarrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction termin�e'
      }
    }

  }
}