podTemplate(label: 'wso2is',
  containers: [containerTemplate(name: 'wso2is', image: 'docker:1.11', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "loitsmiddleware/kubernetes-is"
  node('wso2is') {
    
    def repo = checkout scm 
    
    stage('Build Docker image') {
      container('wso2is') {
      
        
        sh "docker build -f dockerfiles/is/Dockerfile ." 

//       sh "docker build -t ${image} ."
      }
    }
    
    stage('Push to GCR') {
      container('wso2is') {
        sh "docker tag 8ea6460d7499 gcr.io/ipay-project/wso2is"

        sh "docker push gcr.io/ipay-project/wso2is"
      }
    }    
  }
}
