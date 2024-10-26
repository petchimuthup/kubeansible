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
    stage('build docker image') {
      agent {
        label'dockans'
      }
      steps {
        sh 'docker build -t 826316/ansubuntu:new .'
      }
    }
    stage('dockerhub login') {
      agent {
        label 'dockans'
          }
      environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhublogin')
      }
      steps {
        script {
          withDockerRegistry(credentialsId: 'dockerhublogin', toolName: 'docker') {
        sh 'docker push 826316/ansubuntu:new'
      }
    }
      }
    }
    
    stage('kubernetes deploy') {
      agent { 
        label 'kube'}
      steps {
        sh 'kubectl create -f deploy01.yml'
      }
    }
    }
}
  
        
           
         
