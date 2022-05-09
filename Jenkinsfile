pipeline {
    agent any

    stages {
        stage('SCM Check') {
            steps {
                // Get some code from a GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/zahir012/nodejs_project_using_Jenkins_CI-CD_pipelline.git']]])

            }
        }    

        stage('Build docker image') {
            
            steps {
                
                script {
                    
                    sh 'docker build -t zahirul012/nodejs-app-1.0 .'
                }
            }
        }
           
        stage('Deploy to docker') {
            
            steps {
                
                script {
                    
                    sh 'docker run -d --name myweb -p 8989:3000 zahirul012/nodejs-app-1.0'
                }
            }
        }    
        
        stage('Push dokcer image to docker hub') {
            
            steps {
                
                script {
                    
                    withCredentials([string(credentialsId: 'docker', variable: 'docker')]) {
                        
                    sh 'docker login -u zahirul012 -p ${docker}'
                    
}                  
                    sh 'docker push zahirul012/nodejs-app-1.0'
                    
                }
            }
     
        }
        
     stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 zahirul012/nodeja-app-1.0"
 
            }
        }        
        
    }
        post {
            
            always {
                
                sh 'docker logout'
            }
       }
    
}
