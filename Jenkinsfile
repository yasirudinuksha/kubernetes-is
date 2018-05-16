pipeline {
    agent { dockerfile true }
    stages {
        stage('Push') {
            steps {
                sh 'sudo docker push gcr.io/ipay-project/docker.wso2.com/wso2is'
            }
        }
    }
}

