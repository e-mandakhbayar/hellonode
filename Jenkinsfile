node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("releaseworks/hellonode")
    }
    
    stage('Run') {
        steps {
            sh 'docker run -d -p 8000:8000 --name hellonode hellonode'
        }
    }
}

