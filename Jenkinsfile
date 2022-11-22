node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("kubehuzefa/hellonode:${env.BUILD_ID}")
        
    }



    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) 
        {
            sh "sudo docker login -u kubehuzefa -p ${dockerhub}"
        }
        app.push("${env.BUILD_ID}")
       
    }
}
