pipeline {
  agent any
  stages {
    stage('Example') {
      agent any
      environment {
        build_tag = ''
      }
      steps {
        echo 'Hello World'
        sh 'docker build -t zlp/testwebapi:qq1'
      }
    }

  }
}