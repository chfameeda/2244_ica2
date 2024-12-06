pipeline {
    agent any
    stages {
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Git Repo') {
            steps {
                checkout scm
            }
        }
        stage('Clone from repository') {
            steps {
                git url: 'https://github.com/chfameeda/2244_ica2.git', branch: 'develop', credentialsId: 'GIT'
            }
        }

        
stage('Build and run docker image') {
            steps {
                sh 'docker build -t chfameeda3@gmail.com/myapp:latest .'
                sh 'docker stop myapp || true && docker rm myapp || true'
                sh "docker tag chfameeda3@gmail.com/myapp:latest chfameeda3@gmail.com/myapp:develop-${env.BUILD_ID}" 
                sh 'docker run --name myapp -d -p 8081:80 chfameeda3@gmail.com/myapp:latest'
            } 
        }


        stage('Build and Push') {
            steps {
                echo 'Building..'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-auth', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            docker login -u ${USERNAME} -p ${PASSWORD}
                        '''
                      
                    }
            }
        }
        stage('testing') {
            steps {
                sh 'curl -I 3.145.9.207:8080'
            }
        }
       stage('pushing') {
            steps {
                  sh "docker push chfameeda3@gmail.com/myapp:latest"
                  sh "docker push chfameeda3@gmail.com/myapp:develop-${env.BUILD_ID}"
            }
        }
    
    }
}
