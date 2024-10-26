pipeline {
  agent none
  
  stages {
    stage('connect git repo') {
    agent {
        label'dockans'
      }
      steps {
        git([url: 'https://github.com/petchimuthup/kubeansible.git', branch: 'main'])
             }
    }
    
    stage('build docker image and push') {
      agent {
        label 'dockans'
          }
      steps {
        script {
          withDockerRegistry(credentialsId: 'dockerhublogin', toolName: 'docker') {
            sh 'docker build -t 826316/ansubuntu:new .'
            sh 'docker push 826316/ansubuntu:new'
      }
    }
      }
    }
 }
}
  
        
           
         
