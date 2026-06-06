pipeline {
    agent any
    
    triggers {
        githubPush() // S'enclenche automatiquement dès que le Webhook Ngrok reçoit le commit
    }
    
    environment {
        DESTINATAIRE_MAIL = "diaoseydina62@gmail.com"
    }

    stages {
        stage('1. Analyse SAST Semgrep') {
            steps {
                echo 'Initialisation de Semgrep...'
                sh 'docker rm -f semgrep-scanner || true'
                sh 'docker create --name semgrep-scanner -w /src returntocorp/semgrep semgrep scan --config=auto --text -o /src/rapport-sast.txt'
                
                echo 'Analyse du code source cloné automatiquement par Jenkins...'
                sh 'docker cp . semgrep-scanner:/src'
                sh 'docker start -a semgrep-scanner || true'
                
                echo 'Récupération du rapport de vulnérabilités...'
                sh 'docker cp semgrep-scanner:/src/rapport-sast.txt .'
            }
        }
    }

    post {
        always {
            echo 'Envoi du rapport par email...'
            emailext (
                subject: "Rapport DevSecOps - Juice Shop - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: "Le pipeline s'est déclenché automatiquement suite à ton commit.\nStatut : ${currentBuild.currentResult}",
                to: "${DESTINATAIRE_MAIL}",
                attachmentsPattern: 'rapport-sast.txt'
            )
            sh 'docker rm -f semgrep-scanner || true'
        }
    }
}