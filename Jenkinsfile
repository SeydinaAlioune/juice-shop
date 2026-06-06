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
                // Assure-toi que dans Jenkins > Outils, 
                // ton scanner s'appelle bien "SonarScanner"
                script {
                    def scannerHome = tool 'SonarScanner'
                    withSonarQubeEnv('MonServeurSonar') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}