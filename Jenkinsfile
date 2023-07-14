pipeline {
  agent any
  stages {
    stage('Checkout from github') {
      agent any
      steps {
        git(url: 'https://github.com/ddriham/node-hello.git', branch: 'master', credentialsId: 'git-creds', poll: true)
      }
    }

    stage('build_from_Dockerfile') {
      steps {
        sh 'docker build -t ddriham/node-hello:$BUILD_NUMBER . '
      }
    }

    stage('is it working?') {
      steps {
        sh 'docker build - itd --name david_alone -p 3000:3000 ddriham/node-hello:$BUILD_NUMBER'
        sleep 4
        sh 'curl localhost:3000'
        sh 'docker stop david_alone && docker rm david_alone'
      }
    }

    stage('Push_to_DockerHub') {
      parallel {
        stage('Push_to_DockerHub') {
          steps {
            sh 'docker login'
          }
        }

        stage('') {
          steps {
            chuckNorris()
          }
        }

      }
    }

    stage('Clean_workspace') {
      steps {
        cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true)
      }
    }

  }
}