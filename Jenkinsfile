pipeline {
    agent any

    stages {
        stage('Install Docker') {
            steps {
                sh 'curl -fsSL https://get.docker.com -o get-docker.sh'
                sh 'sudo sh get-docker.sh'
                sh 'sudo usermod -aG docker ${USER}' // Add the current user to the docker group
                sh 'sudo systemctl start docker'
                sh 'sudo systemctl enable docker'
            }
        }

        stage('Load Docker Image') {
            steps {
                script {
                    // Load the Docker image from the .tar file
                    sh 'docker load -i /home/tekno/wiregaurd.tar'
                }
            }
        }

        stage('Install Docker Compose') {
            steps {
                sh 'sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
                sh 'sudo chmod +x /usr/local/bin/docker-compose'
                sh 'docker-compose --version'
            }
        }

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
