pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-image'
        VERSION = "v${env.BUILD_NUMBER}"
        REPO = 'jenkins-jb-lab'
        CREDENTIALS_ID = 'docker-yoav'
    }

        stages {
        stage('Build') {
            steps {
                script {
                    sh '''
                    docker build --target test --tag ${IMAGE_NAME}:${VERSION}-test -f welcome/app/bookinfo/src/productpage/Dockerfile welcome/app/bookinfo/src/productpage
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh '''
                    docker build --target test --tag ${IMAGE_NAME}:${VERSION}-test -f welcome/app/bookinfo/src/productpage/Dockerfile welcome/app/bookinfo/src/productpage
                    docker run --rm ${IMAGE_NAME}:${VERSION}-test
                    '''
                }
            }
        }
        }
}