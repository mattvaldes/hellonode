node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line 
         * app = docker.build("mvaldes/jenkins-testing")*/
         sh 'npm install'
    }

    stage('Test image') {
        /*app.inside {
         *   echo "Tests passed"
         *} */
        timeout(time: 5, unit: 'MINUTES') {
            sh """
            echo "BlackDuck Scan..."
            curl -s https://blackducksoftware.github.io/hub-detect/hub-detect.sh > hub-detect.sh
            sh hub-detect.sh
            """
        }   
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused.
         * docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
         *   app.push("${env.BUILD_NUMBER}")
         *   app.push("latest") */
        echo "Push stage"
    }
}
