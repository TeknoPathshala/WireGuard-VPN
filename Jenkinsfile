pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone the Git repository containing your Docker Compose file
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/TeknoPathshala/WireGuard-VPN']]])
            }
        }

        stage('Deploy WireGuard VPN Server') {
            steps {
                script {
                    // Deploy the WireGuard VPN server using Docker Compose directly from the workspace
                    sh 'docker-compose -f docker-compose.yaml up -d'
                }
            }
        }
    }
}
   
