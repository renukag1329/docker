pipeline {
    agent any
 
   
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/renukag1329/docker.git'
             
          }
        }
  
stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t dockerapp:latest .' 
                sh 'docker tag renukag/dockerapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push renukag/dockerapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
            {
                sh "docker run -d -p 8002:8080 renukag/dockerapp"
 
            }
        }
 
    }
 }
