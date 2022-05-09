pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build starting'
        bat 'mvn -B -DskipTests clean package '
        echo 'Build finished'
      }
    }

  }
}