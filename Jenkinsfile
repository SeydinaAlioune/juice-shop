pipeline {
    agent any

    environment {
        // Cette ligne lie le Jenkinsfile à l'outil configuré dans l'interface "Outils"
        SCANNER_HOME = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
    }

    stages {
        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('MonServeurSonar') {
                    // Utilise la variable SCANNER_HOME pour appeler le binaire
                    sh "${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=juice-shop -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sq_ad43b092f774f86d2f0d0a45010c56abfd94f618"
                }
            }
        }
    }
}