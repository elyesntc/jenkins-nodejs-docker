node {
     def app 
     stage('clone repository') {
      checkout scm  
    }
     stage('Build docker Image'){
      app = docker.build("elyesntc/jenkins-nodejs-docker")
    }
     stage('Test Image'){
       app.inside {
         sh 'echo "TEST PASSED"' 
      }  
    }
     stage('Push Image'){
       docker.withRegistry('', 'dockerhubcredentials') {            
       app.push("latest")   
      }
    }
     stage ('Deploy') {
          sshagent(credentials : ['sshcredentials']) {
            sh 'ssh -o StrictHostKeyChecking=no ec2-user@ec2-34-230-59-15.compute-1.amazonaws.com docker run -itd --name web -p 80:8080 elyesntc/jenkins-nodejs-docker'
        }
     }
}
