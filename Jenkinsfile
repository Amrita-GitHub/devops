// node {
//     def app

//     stage('Clone repository') {
//         /* Let's make sure we have the repository cloned to our workspace */

//         checkout scm
//     }

//     stage('Build image') {
//         /* This builds the actual image; synonymous to
//          * docker build on the command line */

//         app = docker.build("Amrita-GitHub/devops")
//     }

//     stage('Test image') {
//         /* Ideally, we would run a test framework against our image.
//          * For this example, we're using a Volkswagen-type approach ;-) */

//         app.inside {
//             sh 'echo "Tests passed"'
//         }
//     }

//     stage('Push image') {
//         /* Finally, we'll push the image with two tags:
//          * First, the incremental build number from Jenkins
//          * Second, the 'latest' tag.
//          * Pushing multiple tags is cheap, as all the layers are reused. */
//         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {

//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//         }
//     }
// }


node {
    def app

    stage('Clone repository') {
        // Checkout the repository into the workspace
        checkout scm
    }

    stage('Build image') {
        // Build the Docker image (similar to 'docker build')
        app = docker.build("Amrita-GitHub/devops")
    }

    stage('Test image') {
        // Convert Windows workspace path to Linux-style path
        def linuxWorkspace = env.WORKSPACE
                            .replaceAll('\\\\', '/')       // Replace backslashes with forward slashes
                            .replaceAll(/^([A-Za-z]):/, '/$1')  // Convert drive letter (e.g. C:) to /C
                            .toLowerCase()
        echo "Using Linux workspace path: ${linuxWorkspace}"

        // Run the container with a Linux-compatible working directory and volume mapping
        app.inside("-w /workspace -v ${linuxWorkspace}:/workspace") {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
<<<<<<< HEAD
        // Push the image to Docker Hub with two tags
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
=======
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {

>>>>>>> e0379fbe344015789ba839dd575da9e566909cb0
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
