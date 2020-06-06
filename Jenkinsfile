pipeline {
    agent any
    stages {
        stage('Lint') {
            steps {
                sh 'echo "Linting dockerfile"'
                sh 'hadolint-Linux-x86-64 Dockerfile'
                sh '/usr/local/bin/pylint/pylint --disable=R,C,W1203,E1120 app.py'                
            }
        }


        stage('Build image') {
            steps {
                sh 'echo "building and pushing docker image"'

                script {
                    withDockerRegistry(credentialsId: 'jenkinscred', url: '') {
                        def customImage = docker.build("jansdockerhub/streamlit-test:${env.BUILD_ID}")
                        customImage.push('latest')
                    }
                }
            }
        }


        stage('Deploy image') {
            steps {
                sh 'kubectl run streamlit-test --image=jansdockerhub/streamlit-test --port=8080'
            }
        }
        
    }
}