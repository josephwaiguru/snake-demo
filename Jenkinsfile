pipeline {
   agent any
   stages {  
    
    stage('Cloning Git') {
       steps 
         {
            /* Let's make sure we have the repository cloned to our workspace */
            checkout scm
         }
    }  
    stage('SAST'){
        steps {
            build 'SECURITY-SAST-SNYK'
        }
    }

    
    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        steps {
	sh 'echo Build and Tag'
        }
    }
    stage('Post-to-dockerhub') {
      steps {
     # docker.withRegistry('https://registry.hub.docker.com', 'training_creds') {
       #     app.push("latest")
        #			}
       sh 'echo post to dockerhub repo'
      }
    }
    stage('SECURITY-IMAGE-SCANNER'){
       steps {
	 sh 'echo scan image for security'
         # build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
       }
    }
  
    
    stage('Pull-image-server') {
      steps {
         sh 'echo pulling image ...'
         #sh "docker-compose down"
         #sh "docker-compose up -d"	
      }
    }
    
    stage('DAST') {
       steps {
         sh 'echo dast scan for security'
         build 'SECURITY-DAST-OWASP_ZAP'
        }
    }
 }
}
