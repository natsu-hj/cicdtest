pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/natsu-hj/cicdtest.git', branch: 'master'
      }
    }
    stage('blog update') {
      steps {
        sh '''
        sudo echo "<br> blog page!!" >> index.html
        '''
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t natsunohj/testweb:newnewblog .
        sudo docker push natsunohj/testweb:newnewblog
        '''
      }
    }
    stage('shop update') {
      steps {
        sh '''
        sudo sed -i 's/blog/shop' index.html
        '''
      }
    }
    stage('docker build and push new') {
      steps {
        sh '''
        sudo docker build -t natsunohj/testweb:newnewshop .
        sudo docker push natsunohj/testweb:newnewshop
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
        sudo kubectl set image deploy deploy-blog ctn-blog=natsunohj/testweb:newnewblog
        sudo kubectl set image deploy deploy-shop ctn-shop=natsunohj/testweb:newnewshop
        '''
      }
    }
  }
}
