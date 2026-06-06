pipeline {
    agent any

    // C'est cette partie qui répare le déclenchement automatique de tes builds !
    triggers {
        pollSCM('* * * * *')
    }

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
                        // On force l'URL ici pour régler le problème "localhost"
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=http://host.docker.internal:9000"
                    }
                }
            }
        }
    }
}