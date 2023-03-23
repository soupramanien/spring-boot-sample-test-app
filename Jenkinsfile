pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va dÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â©marrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction terminÃƒÆ’Ã†â€™Ãƒâ€šÃ‚Â©e'
        archiveArtifacts '**/target/*.jar'
        sh 'docker build -t testapp:latest -v $(which docker):/usr/local/bin/docker'
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Test unitaire va dÃƒÆ’Ã‚Â©marrer'
            sh 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            echo 'test unitaire terminÃƒÆ’Ã‚Â©'
            junit '**/target/surefire-reports/TEST-*.xml'
          }
        }

        stage('Integration') {
          steps {
            echo 'est d\'integration va dÃƒÂ©marrer'
            sh 'mvn -Dtest="com.example.testingweb.integration.**" test'
            echo 'test d\'integration terminÃƒÂ©'
          }
        }

        stage('Functional') {
          steps {
            echo 'test fonctionnel va demarrer'
            sh 'mvn -Dtest="com.example.testingweb.functional.**" test'
            echo 'test fonctionnel terminÃ©'
          }
        }

      }
    }

    stage('Deploy') {
      when {
        expression {
          currentBuild.result == null || currentBuild.result == 'SUCCESS'
        }

      }
      steps {
        input(message: 'Voulez-vous continuer ?', ok: 'Alons-y')
        echo 'déploiement va démarrer'
        sh 'docker run -d -p 3030:9090 testapp:latest -v $(which docker):/usr/local/bin/docker'
        echo 'déploiement terminé'
      }
    }

  }
  tools {
    maven 'maven 3.8'
  }
  post {
    success {
      emailext(to: 'soupramanien@baobab-ingenierie.fr', subject: "${env.BUILD_ID} - ${currentBuild.result}", body: "${env.BUILD_ID} - ${env.JENKINS_URL}")
    }

  }
}