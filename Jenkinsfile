pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials("DHubCred")
    }
    agent {
        label 'K-M'
    }

    stages {
        stage('scm') {
            steps {
                git branch: 'main', url: 'https://github.com/shahfahed/Project-1'
            }
        }
        stage('docker') {
            steps {
                sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                sh 'sudo docker build --file Dockerfile --tag shahfahed/project-1:$BUILD_NUMBER .'
                sh 'sudo docker push shahfahed/project-1:$BUILD_NUMBER'
            }
        }
        stage('k8s') {
            steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl apply -f np-svc.yaml'
            }
        }
    }
}
