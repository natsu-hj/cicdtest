pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/natsu-hj/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t natsunohj/testweb:newnewmain .
        sudo docker push natsunohj/testweb:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
	sudo kubectl set iamge deploy deploy-main ctn-main=natsunohj/testweb:newnewmain
        '''
      }
    }
  }
}
