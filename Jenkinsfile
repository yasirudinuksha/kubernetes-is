podTemplate(label: 'wso2is',
  containers: [containerTemplate(name: 'wso2is', image: 'docker:1.11', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "kubernetes-is"
  node('wso2is') {
    
    def repo = checkout scm 
    
    stage('Build Docker image') {
      container('wso2is') {
      
        
       // ** sh "docker build -f dockerfiles/is/Dockerfile ." 

//       sh "docker build -t ${image} ."
        
        sh "docker build -t ${image} -f dockerfiles/is/Dockerfile ."
      }
    }
    
    stage('Push to GCR') {
      container('wso2is') {
        //sh "docker tag 8ea6460d7499 gcr.io/ipay-project/wso2is"
        //sh "gcloud auth configure-docker"
        //sh "docker push gcr.io/ipay-project/wso2is"
        sh "gcloud auth configure-docker"
        sh "docker tag ${image} gcr.io/ipay-project/wso2is"
        sh "docker push gcr.io/ipay-project/wso2is"
      }
    }    
  }
}
