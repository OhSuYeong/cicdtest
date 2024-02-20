pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/OhSuYeong/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t ohsuyeong/cicdtest:green .
        sudo docker push ohsuyeong/cicdtest:green
        '''

      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        export KUBECONFIG=/etc/kubernetes/admin.conf && kubectl create deployment pl-bulk-prod --image=ohsuyeong/cicdtest:green
        export KUBECONFIG=/etc/kubernetes/admin.conf && kubectl expose deployment pl-bulk-prod --type-LoadBalancer --port=8080 \
                                                                   --target-port=80 --name=pl-bulk-prod-
        '''
      }
    }
  }
}
