node ('prod') {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build images') {
        /* This builds the actual image; synonymous to
         * docker build on the command line. */
             echo "${env.BUILD_NUMBER}"
             sh 'docker build -t saddamclas/website-jenkins-pipeline -f website . '
    }
    stage('Push Image') {
           /* docker.withRegistry('https://registry.hub.docker.com', 'ec6095eb-472e-419b-ad61-8454d3afb61c')*/
        withDockerRegistry([ credentialsId: "38215e39-4faf-48d8-95eb-5f9df1a821e8", url: "" ]) {
            echo "${env.BUILD_NUMBER}"
            sh "docker tag saddamclas/website-jenkins-pipeline saddamclas/website-jenkins-pipeline:${env.BUILD_NUMBER}" 
            sh "docker push saddamclas/website-jenkins-pipeline:${env.BUILD_NUMBER}"
            }
    }
    stage('Deploy ') {  
          /*  sh " docker srevice create --name web -p 9089:80  linuxcloudops/website-test:${env.BUILD_NUMBER}"  */
         sh "docker stack deploy -c  docker-stack.yml wesite"
         }
} 

