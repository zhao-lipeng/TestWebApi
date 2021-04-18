pipeline {
  agent any
  stages {
    stage('Prepare') {
      agent any
      environment {
        build_tag = ''
      }
      steps {
        script {
          build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()

          build_tag = "${BRANCH_NAME}-${build_tag}"

          echo "${build_tag}"
        }

      }
    }

    stage('BuildImage') {
      steps {
        sh 'docker build -f ./TestWebApi/Dockerfile   -t zlp/testwebapi:${build_tag} .'
      }
    }

  }
  environment {
    build_tag = ''
  }
}