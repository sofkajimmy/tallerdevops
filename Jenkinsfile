pipeline {
   agent { label 'agent1' }
    
    stages {        
        stage('build') {            
            steps {
                sh 'docker build -t kamentsa/tallerdevops:${BUILD_NUMBER}  .'                 
            }
        }
        stage('push') {            
            steps {
                
                 withDockerRegistry([ credentialsId: "dockerhublocal", url: "" ]) {
                    sh 'docker push kamentsa/tallerdevops:${BUILD_NUMBER}'                 
                }   
                
            }
        }
        
        stage('Deploy') {            
            steps {
                sh ' kubectl apply -f k8s/'
                sh ' kubectl get all -n tallerdevops'                 
            }
        }
    }
}