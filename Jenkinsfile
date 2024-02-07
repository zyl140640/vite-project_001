//Jenkinsfile
pipeline {
    agent any

    // 环境变量，可以根据实际情况进行配置
    environment {
        GIT_URL = 'https://github.com/zyl140640/vite-project_001.git'
        CREDENTIALS_ID = 'ac22058b-51b5-40f3-8420-80bf7e1b7771'
        SSH_CREDENTIALS_ID = '192.168.110.210'
        REMOTE_DIR = 'D:\\vue_app' // 远程Windows服务器上的目标目录，使用双斜杠
    }

    stages {
        // 从Git仓库获取代码
        stage('Checkout') {
            steps {
                git credentialsId: "${CREDENTIALS_ID}", url: "${GIT_URL}"
            }
        }

        // 安装依赖并构建Vue.js应用
        stage('Build') {
            steps {
                script {
                    // 安装依赖
                    sh 'npm install'
                    // 构建应用
                    sh 'npm run build'
                }
            }
        }

        // 将构建结果上传到远程服务器
        stage('Deploy') {
            steps {
                script {
                    // 使用Publish Over SSH插件上传文件并在Windows服务器上执行命令
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: "${SSH_CREDENTIALS_ID}",
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'dist/**/*',
                                        removePrefix: 'dist',
                                        remoteDirectory: "${REMOTE_DIR}",
                                        execCommand: "powershell -Command \"Expand-Archive -Path '${REMOTE_DIR}\\dist.zip' -DestinationPath '${REMOTE_DIR}' -Force; Remove-Item -Path '${REMOTE_DIR}\\dist.zip' -Force\""
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }

        // 在服务器上进行最终部署步骤（可选）
        stage('Finalize Deployment') {
            steps {
                script {
                    // 使用SSH执行Windows命令，例如重启Windows服务
                    sshagent(credentials: ["${SSH_CREDENTIALS_ID}"]) {
                        sh "ipconfig "
                    }
                }
            }
        }
    }
}
