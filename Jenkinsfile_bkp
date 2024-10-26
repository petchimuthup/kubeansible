pipeline {
    agent {label 'kube'}
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        KUBE_CONFIG = credentials('aws-kubeconfig') 
        ANSIBLE_INVENTORY = '/home/jenkins/workspace/kubedeploy/k8s_inventory.ini' 
          }
    stages {
      stage('run kubernetes deployment') {
        steps {
          sh 'kubectl create -f deploy01.yml'
        }
      }
      stage('Run Ansible Playbook on Kubernetes Pods') {
            steps {
                script {
                    sh '''
                    ansible-playbook -i ${ANSIBLE_INVENTORY} install_packages.yml \
                    --extra-vars "kubeconfig_path=${WORKSPACE}/aws-kubeconfig"
                    '''
                }
            }
        }
    }
}
