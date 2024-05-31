node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("releaseworks/hellonode:${BUILD_ID}")
    }

    stage('Run') {
        
            script {
                // Stop and remove the existing container if it's running
                def existingContainer = sh(script: "docker ps -q --filter name=myapp-container", returnStdout: true).trim()
                if (existingContainer) {
                    sh "docker stop myapp-container"
                    sh "docker rm myapp-container"
                }
                // Run the new container
                sh "docker run -d -p 8000:8000 --name myapp-container releaseworks/hellonode:${BUILD_ID}"
            }
    }
}
