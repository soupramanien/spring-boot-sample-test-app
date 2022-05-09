pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'La construction va dÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â©marrer'
        sh 'mvn -DskipTests clean package'
        echo 'la construction terminÃƒÆ’Ã†â€™Ãƒâ€šÃ‚Â©e'
        archiveArtifacts '**/target/*.jar'
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
        sh 'mvn -DskipTests install'
        echo 'déploiement terminé'
      }
    }

  }
  post{
    success{
      mail to: "eliott.mischler@grenoble-em.com" 
    }
  }
  tools {
    maven 'maven 3.8'
  }
}