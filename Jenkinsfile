pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "myapp:latest"
    }

    stages {
        stage('Setup') {
            steps {
                sh 'echo $PATH'
                sh 'docker --version'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    def existingContainer = sh(script: "docker ps -q --filter name=myapp-container", returnStdout: true).trim()
                    if (existingContainer) {
                        sh "docker stop myapp-container"
                        sh "docker rm myapp-container"
                    }
                    sh "docker run -d -p 8000:8000 --name myapp-container ${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        always {
            sh "docker system prune -f"
        }
    }
}
