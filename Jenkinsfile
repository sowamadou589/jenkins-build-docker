node {
    def app
    def dockerHostIP = "192.168.77.2"  // IP de l’hôte Docker vue depuis Jenkins

    stage('Clone') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("xavki/nginx")
    }

    stage('Run image') {
        docker.image('xavki/nginx').withRun('-p 81:80') { c ->
            sh 'docker ps'
            sh "curl http://${dockerHostIP}:81"
        }
    }
}
