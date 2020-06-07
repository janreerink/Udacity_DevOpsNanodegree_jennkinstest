pipeline {
    agent any
    stages {
        

        stage('Deploy image') {
            steps {
                //sh "/usr/bin//kubectl cluster-info"
                sh "echo $KUBECONFIG"
                sh "kubectl version"
                sh "kubectl get nodes"
                //sh "kubectl run nginx  --replicas=2 --labels='app=nginx' --image=nginx --port=80"
                //sh "kubectl run streaml --labels='app=streamlit-test' --image=jansdockerhub/streamlit-test:${env.BUILD_ID} --port=8501"
                //sh 'kubectl create -f loadbalancer.yaml'
                //kubectl get service/strlit-service |  awk {'print $1" " $2 " " $4 " " $5'} | column -t
            }
        }
        
    }
}