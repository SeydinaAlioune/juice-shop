pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    environment {
        // Cela utilise l'outil configuré dans Jenkins (Administrer Jenkins > Outils)
        SCANNER_HOME = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
    }

    stages {
        stage('Analyse SonarQube') {
            steps {
                echo 'Début de l\'analyse SonarQube...'
                withSonarQubeEnv('MonServeurSonar') {
                    // host.docker.internal pointe vers ton PC hôte depuis le conteneur Jenkins
                    sh '${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=juice-shop -Dsonar.sources=. -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.login=sq_ad43b092f774f86d2f0d0a45010c56abfd94f618'
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