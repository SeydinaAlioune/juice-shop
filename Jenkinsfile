pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'
                    withSonarQubeEnv('MonServeurSonar') {
                        // On force l'URL ici pour éviter l'erreur localhost
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=http://host.docker.internal:9000"
                    }
                }
            }
        }
    }
}