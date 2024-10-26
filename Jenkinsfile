pipeline {
  agent none
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhublogin')
    ANSIBLE_HOST_KEY_CHECKING = 'False'
    KUBE_CONFIG = credentials('kubeconfig')
    ANSIBLE_INVENTORY = '/home/jenkins/workspace/gitdockanskube/k8inventory.ini'
  }
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
      steps {
        script {
          withDockerRegistry(credentialsId: 'dockerhublogin', toolName: 'docker') {
        sh 'docker push 826316/ansubuntu:new'
      }
    }
      }
    }
    
    stage('kubernets deploy') {
      agent { 
        label 'kube'}
      steps {
        sh 'kubectl create -f deploy.yml'
      }
    }
    }
}
  
        
           
         
