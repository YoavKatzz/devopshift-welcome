pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-docker-image'
        VERSION = "v${env.BUILD_NUMBER}"
        REPO = 'yoavkatz/jenkins-jb-lab'
        CREDENTIALS_ID = 'docker_yoav'
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
        stage('Push') {
            steps {
                script {
                    docker.withRegistry("https://index.docker.io/v1/", "${CREDENTIALS_ID}") {
                        sh '''
                        docker push ${REPO}/${IMAGE_NAME}:${VERSION}-test
                        docker tag ${REPO}/${IMAGE_NAME}:${VERSION}-test ${REPO}/${IMAGE_NAME}:latest

                        '''
                    }
                }
            }
        }
        }
}