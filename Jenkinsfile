node {
    def app

    stage('Clone') {
        // Clone le code source à partir de SCM
        checkout scm
    }
    
    stage('Build image') {
        // Build l'image Docker en utilisant le Dockerfile du répertoire actuel
        app = docker.build("xavki/nginx")
    }
    
    stage('Run image') {
        // Lance l'image Docker en exposant le port 80 sur le port 81 de la machine hôte
        docker.image('xavki/nginx').withRun('-p 81:80') { c ->
            // Liste les containers en cours d'exécution
            sh 'docker ps'
            
            // Envoie une requête HTTP GET vers le serveur Nginx en cours d'exécution dans le container
            sh 'curl localhost:81'
        }
    }
}

