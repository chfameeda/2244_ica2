
pipeline {
    agent any
    stages {
        
stage('Build and run docker image') {
            steps {
                
                sh 'docker stop myapp || true && docker rm myapp || true'
                sh "docker pull fameeda941888/myapp:latest" 
                sh 'docker run --name myapp -d -p 8082:80 fameeda941888/myapp:latest'
            } 
        }


      
        stage('testing') {
            steps {
                sh 'curl -I 3.145.9.207:8082'
            }
        }
      
    }
}
