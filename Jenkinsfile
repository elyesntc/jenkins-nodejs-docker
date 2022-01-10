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
            sh 'ssh -o StrictHostKeyChecking=no elyes@localhost uptime'
        }
     }
}
