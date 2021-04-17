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
        script {
          def browsers = ['chrome', 'firefox']
          for (int i = 0; i < browsers.size(); ++i) {
            echo "Testing the ${browsers[i]} browser"
          }
        }

        script {
          build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
          if (env.BRANCH_NAME != 'master') {
            build_tag = "${env.BRANCH_NAME}-${build_tag}"
          }
        }

        echo '${env.build_tag}'
      }
    }

  }
}