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
        ansible master -m shell -a 'export KUBECONFIG=/etc/kubernetes/admin.conf && kubectl create deploy web-green --replicas=3 --image=ohsuyeong/cicdtest:green'
        ansible master -m shell -a 'export KUBECONFIG=/etc/kubernetes/admin.conf && kubectl expose deploy web-green --type=LoadBalancer --port=80 --target-port=80 --name=web-green-svc'
      }
    }
  }
}
