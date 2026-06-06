pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Analyse SonarQube') {
            steps {
                echo 'Début de l\'analyse SonarQube...'
                // Utilise la configuration 'MonServeurSonar' définie dans Jenkins
                withSonarQubeEnv('MonServeurSonar') {
                    // Remplace le login par ton token réel
                    sh 'sonar-scanner -Dsonar.projectKey=juice-shop -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sq_ad43b092f774f86d2f0d0a45010c56abfd94f618'
                }
            }
        }
    }

    post {
        always {
            echo 'Analyse terminée. Vérifiez les résultats sur http://localhost:9000'
        }
    }
}