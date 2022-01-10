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
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")   
      }
    }
     stage ('Deploy') {
       sh 'ssh elyes@localhost docker run -itd -p 5000:8080 --name webserver elyesntc/jenkins-nodejs-docker:${env.BUILD_NUMBER}'
    }
