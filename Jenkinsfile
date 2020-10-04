#!groovy

pipeline {
     agent any
    //  使用docker安装node
    // agent {
    //     docker { image 'node:14-alpine' }
    // }

    tools {
        nodejs 'NodeJS 11.5.0'
        gradle "gradle"
    }
    // 指定一个小时的全局执行超时，之后Jenkins将中止Pipeline运行
    options {
        timeout(time: 1, unit: 'HOURS') 
    }
    // environment { 
    //     CC = 'clang'
    // }
//定期检查开发代码自动触发更新，工作日每晚4点做daily build
    triggers {
        pollSCM('H 4 * * 1-5')
    }
    stages {

         stage('init') {
           steps {
            script{
              def dockerPath = tool 'docker' //全局配置里的docker
              env.PATH = "${dockerPath}/bin:${env.PATH}" //添加了系统环境变量上
            }
           }
    }

    stage('Build') {
        steps {
            script{
              sh "docker --version"
            }
        }
    }
        // stage('checkout') {
        //     steps {

        //         // echo '$env.GIT_BRANCH'
        //          echo 'This is a pullCode step'
        //             // 从环境变量中获取git分支
        //         echo env.BRANCH_NAME
        //         //  checkout scm
        //         // git url: 'https://github.com/zmmsdk/baka.git', branch:env.BRANCH_NAME

        //     //    git "checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '9ca5cd04-7144-4578-a9f7-695064523a15', url: 'https://github.com/zmmsdk/baka.git']]])"
        //     }
        // }
  
         stage('Linting') {
            steps {
               script {
                sh 'npm config set registry https://registry.npm.taobao.org' 
                sh 'npm config get registry' 
                // sh 'cnpm install'
                sh 'npm install'
                sh 'npm run build'
               }
            }
        }   
        // stage('build') {
        //     steps {
        //        script {
             
        //        }
        //     }
        // }  
        stage('unit test') {
            steps {
            echo 'This is a test step'
         
            //    sh "npm  test"
            //    sh 'ls -al coverage/'
            }
        }      
         stage('Quality scanning') {
            steps {
            echo 'This is a test step'
         
            //    sh "npm  test"
            //    sh 'ls -al coverage/'
            }
        }     
         stage('Build image and push') {
            steps {
            echo 'This is a test step'
         
            //    sh "npm  test"
            //    sh 'ls -al coverage/'
            }
        }    
         stage('image scanning') {
            steps {
            echo 'This is a test step'
         
            //    sh "npm  test"
            //    sh 'ls -al coverage/'
            }
        }     
         stage('Deploy') {
            steps {
            echo 'This is a test step'
         if (env.BRANCH_NAME == 'master') {
            echo 'I only execute on the master branch'
        } else if(env.BRANCH_NAME == 'dev-0.8'){
             echo 'I only execute on the dev branch'
        }else if(env.BRANCH_NAME == 'sit-0.8'){
             echo 'I only execute on the sit branch'
        }else if(env.BRANCH_NAME == 'uat-0.8'){
             echo 'I only execute on the uat branch'
        }
        else {
            echo 'I execute elsewhere'
        }
            }
        }   
    }

    post {
        always {
            deleteDir()
            script {
                sh 'echo "post handling"'
            }

            // unsuccessful {
            //     step([$class:'Mailer',notifyEveryUnstableBuild:true,recipients: 'a972332466@163.com',sendToIndividuals:true])
            // }
        }
        // success {
        //     echo '构建成功'
        // }
        // failure {
        //     echo '构建失败'
        // }
        // unstable {
        //     echo '该任务被标记为不稳定任务'
        // }
        // aborted {
        //     echo '该任务被终止' 
        // }
    }


}



// if (env.BRANCH_NAME == 'master' || env.BRANCH_NAME == null) {
//                 timeout(time: 10, unit: 'MINUTES') {
//                       input '确认要部署线上环境吗？'
//     }