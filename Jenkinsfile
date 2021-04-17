#!/usr/bin/env groovy
pipeline{
 agent any
    // 可以设置环境变量
 environment {
        PATH = "/home/testhadoop/.pyenv/shims:$PATH"
        runEnv = 'server'
    }
    //默认命令运行的pwd 为项目workspace
    stages {
        stage('Build') {
            steps{
                echo '='*50 + '开始构建' + '='*50
                echo '---> 更新依赖包'
                sh 'pipenv install --skip-lock'
                echo '---> 扫描用例信息'
                sh 'pipenv run python case_scanner.py'
                echo 'build success!'
             }
        }
        // stage可以添加或减少
        stage('Test') {
            steps{
                echo 'This is a test step!'
            }
        }
        stage('Deploy') {
            steps{
                echo 'This is a deploy step'
            }
        }
    }
 post {
     failure{
            script{
                emailext attachLog: true,
                // 邮件模板这里的引号一定要注意写对（坑）
                body: '''${SCRIPT, template="groovy-html.template"}''',
                mimeType: 'text/html',
                charset:'UTF-8',
                // PlatformGroup #10 构建失败
                subject: "${currentBuild.fullDisplayName} 构建失败",
                //用逗号或空格分隔多个邮箱
                to: 'xxx@xx.com xxxx@xxx.com'
         }
     }
 }
}