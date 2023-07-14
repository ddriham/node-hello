pipeline {
  agent any
  stages {
    stage('Check out from github') {
      steps {
        git(url: 'https://github.com/ddriham/node-hello.git', branch: 'master', poll: true, credentialsId: '	git-creds')
      }
    }

    stage('build the image ftom dokerfile') {
      steps {
        sh 'docker build -t ddriham/node-hello:$BUILD_NUMBER .'
      }
    }

    stage('Run the Container') {
      steps {
        sh 'docker run -itd --name node-hello -p 3000:3000 ddriham/node-hello:$BUILD_NUMBER'
        sleep 5
      }
    }

    stage('test the app') {
      steps {
        sh 'curl localhost:3000'
        sh 'docker stop node-hello && docker rm node hello'
      }
    }

    stage('push to DockerHub') {
      steps {
        sh 'docker login'
      }
    }

  }
}