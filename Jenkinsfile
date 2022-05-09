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

  }
  tools {
    maven 'maven 3.8'
  }
}