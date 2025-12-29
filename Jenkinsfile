pipeline {
    // 指定在任何可用的 Jenkins 节点上运行
    agent any

    stages {
        // 第一阶段：准备环境
        stage('准备阶段') {
            steps {
                echo '🔍 检查系统环境...'
                sh 'java -version' // 执行 Shell 命令查看 Java 版本
                echo '✅ 环境检查完毕。'
            }
        }

        // 第二阶段：构建应用
        stage('构建阶段') {
            steps {
                echo '🏗️ 正在编译代码...'
                echo '📦 正在打包生成文件 (Artifact)...'
                // 这里可以放置具体的打包命令，如 sh 'mvn clean package'
            }
        }

        // 第三阶段：自动化测试
        stage('测试阶段') {
            steps {
                echo '🧪 启动单元测试...'
                sh 'echo "Running tests..." '
                echo '✔️ 所有测试用例已通过。'
            }
        }

        // 第四阶段：发布部署
        stage('部署阶段') {
            steps {
                echo '🚀 正在上传文件到生产服务器...'
                echo '🌐 服务已启动：http://localhost:8080'
            }
        }
    }

    // 后置处理：构建结束后的动作
    post {
        always {
            echo '🧹 正在清理临时文件...'
        }
    }
}