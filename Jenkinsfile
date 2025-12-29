pipeline {
    agent any

    // 1. 定义工具：自动引入 Maven 和 JDK (需在 Jenkins 全局工具配置中预设名称)
    tools {
        maven 'Maven 3.9.5'
        jdk 'JDK 17'
    }

    // 2. 定义环境变量：避免硬编码，便于后期维护
    environment {
        APP_NAME    = 'M78-Security-Demo'
        APP_VERSION = '1.0.0-SNAPSHOT'
        GIT_REPO    = 'git@github.com:guguji666666/M78Jenkins.git'
        MAVEN_OPTS  = '-Xmx1024m'
    }

    // 3. 运行选项：设置日志保留、禁止并行构建、超时时间
    options {
        buildDiscarder(logRotator(numToKeepStr: '10')) // 保留最近10次构建
        disableConcurrentBuilds()                     // 禁并行，防止资源竞争
        timeout(time: 1, unit: 'HOURS')               // 超时自动停止
        timestamps()                                  // 在日志中显示时间戳
    }

    stages {
        // 第一步：拉取代码 (优化：使用 checkout 插件而非手动 sh git clone)
        stage('Pulling Source') {
            steps {
                echo "🚀 Starting Checkout for ${APP_NAME}..."
                checkout scmGit(
                    branches: [[name: '*/main']], 
                    extensions: [], 
                    userRemoteConfigs: [[url: "${env.GIT_REPO}"]]
                )
            }
        }

        // 第二步：代码检查 (模拟安全审计，符合你的专业背景)
        stage('Security Scan') {
            steps {
                echo '🛡️ Running Security Analysis...'
                // 示例：此处可以集成 SonarQube 或简单的依赖扫描
                sh 'echo "Scanning for vulnerabilities..."'
            }
        }

        // 第三步：Maven 构建
        stage('Build Artifact') {
            steps {
                echo '📦 Building JAR file...'
                sh 'mvn clean package -DskipTests'
            }
        }

        // 第四步：单元测试 (保证代码质量)
        stage('Unit Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml' // 生成测试报告
                }
            }
        }

        // 第五步：归档或 Docker 构建
        stage('Dockerize & Push') {
            steps {
                echo '🐳 Building Docker Image...'
                // 示例：基于你的 Home Server 或 Docker 实验室环境
                // sh "docker build -t ${APP_NAME}:${APP_VERSION} ."
            }
        }
    }

    // 4. 后置处理：无论成功失败都发出通知
    post {
        success {
            echo "✅ Great Success! ${APP_NAME} has been deployed."
        }
        failure {
            echo "❌ Mission Failed! Ultraman Ace, please check the logs."
        }
    }
}