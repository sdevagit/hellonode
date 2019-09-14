node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("firstjenkinssetup/hellonode")
    }

    stage('Verify image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

     stage('Push image') {
        docker.withRegistry('https://153627826700.dkr.ecr.eu-west-1.amazonaws.com/firstjenkinssetup', 'ecr:eu-west-1:demo-ecr-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    } 
}
