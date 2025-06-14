pipeline {
    agent any

    environment {
        IMAGE_NAME = 'springboot-docker'
        CONTAINER_NAME = 'springboot-docker-container'
        PORT = '8080'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 GitHub 소스 체크아웃'
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                echo '📦 Maven 빌드 중...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🔨 Docker 이미지 빌드 중...'
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop Existing Container') {
            steps {
                echo '🛑 기존 컨테이너 중지 및 삭제'
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
            }
        }

        stage('Run Docker Container') {
            steps {
                echo '🚀 Docker 컨테이너 실행 중...'
                sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:8080 ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo '✅ 배포 성공!'
        }
        failure {
            echo '❌ 배포 실패. 로그 확인 요망.'
        }
    }
}
