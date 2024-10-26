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
            sh 'docker build -t 826316/ansubuntu .'
            sh 'docker push 826316/ansubuntu'
      }
    }
      }
    }
    stage('deploy image in kubernetes') {
      environment {
        KUBE_CONFIG = credentials('kubeconfig')
      }
      agent {
        label 'kube'
      }
      steps {
        sh 'kubectl create -f deploy01.yml'
      }
        
 }
}
  
        
           
         
