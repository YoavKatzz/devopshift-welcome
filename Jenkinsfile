pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-jb-lab'
        VERSION = "v${env.BUILD_NUMBER}"
        REPO = 'yoavkatz'
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
                        '''
                    }
                }
            }
        }
        }
}