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
        ansible master -m copy -a 'src=a.yaml dest=/root/a.yaml'
        ansible master -m shell -a 'export KUBECONFIG=/etc/kubernetes/admin.conf && kubectl apply -f /root/a.yaml'
      }
    }
  }
}
