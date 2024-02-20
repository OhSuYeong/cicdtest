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
        docker build -t ohsuyeong/cicdtest:green .
        docker push ohsuyeong/cicdtest:green
        '''

      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deployment pl-bulk-prod --image=ohsuyeong/cicdtest:green
        kubectl expose deployment pl-bulk-prod --type-LoadBalancer --port=8080 \
                                                                   --target-port=80 --name=pl-bulk-prod-
        '''
      }
    }
  }
}
