pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Jenkins utilise ici les credentials configurés
                checkout scm
            }
        }

        stage('Analyse SonarQube') {
            steps {
                // Utilise le nom 'MonServeurSonar' configuré dans l'admin système
                withSonarQubeEnv('MonServeurSonar') {
                    // Lance le scanner SonarQube
                    sh 'sonar-scanner -Dsonar.projectKey=juice-shop -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=$SONAR_AUTH_TOKEN'
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo "Analyse terminée et envoyée à SonarQube."
            }
        }
    }
}