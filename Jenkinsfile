pipeline {
    agent any  // Utilisez n'importe quel agent Jenkins disponible

    stages {
        stage('Checkout Code') {
            steps {
                // Récupère le code source depuis le référentiel en utilisant le jeton d'authentification
                checkout([$class: 'GitSCM', branches: [[name: 'adem_wertani_5SIM3_G5']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CloneOption', credentialsId: 'PAT_JENKINS']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/ademwertani/5SIM3_G5_projet4.git']]])
            }
        }
        
        stage('Build with Maven') {
            steps {
                // Exécutez la commande Maven pour nettoyer et compiler
                sh 'mvn clean install'  // Assurez-vous que Maven est configuré dans Jenkins
            }
        }
    }
    
    post {
        success {
            // Actions à exécuter en cas de succès (par exemple, notification par e-mail)
            emailext(
                subject: "Build réussi",
                body: "Le build a réussi avec succès.",
                to: 'adem.wertani@esprit.tn',
            )
        }
        failure {
            // Actions à exécuter en cas d'échec (par exemple, notification par e-mail d'échec)
            emailext(
                subject: "Échec du build",
                body: "Le build a échoué. Veuillez vérifier les logs Jenkins pour plus d'informations.",
                to: 'adem.wertani@esprit.tn',
            )
        }
    }
}
