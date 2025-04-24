node {
    def container

    stage('Build Docker Image') {
        container = docker.build("mon-nginx-test")
    }

    stage('Run and Test Container') {
        docker.image('mon-nginx-test').withRun('-d -P') { c ->
            // Affiche les conteneurs en cours
            sh 'docker ps'

            // Récupère l'adresse IP du conteneur
            def ip = sh(
                script: "docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ${c.id}",
                returnStdout: true
            ).trim()

            echo "IP du conteneur : ${ip}"

            // Fait un curl sur le serveur nginx à l’intérieur du conteneur
            sh "curl http://${ip}:80"
        }
    }
}
