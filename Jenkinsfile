pipeline {
  agent any
  
  stages{
     
   
    stage('SSH into the server') {
        steps {
               script {
                            def remote = [:]
                            remote.name = 'K8S Node2'
                            remote.host = '172.20.5.68'
                            remote.user = 'patiwat'
                            remote.password = 'patiwat#123'
                            remote.allowAnyHosts = true
                 
                 
                 echo 'SSH Success...!!'
                 
                 stage('Using Command Docker Bulid && Tag') {
                        
                        //sshCommand remote: remote, command: "pwd"
                        //sshCommand remote: remote, command: "whoami"
                        sshCommand remote: remote, command: "git clone https://github.com/patiwat13/patiwat13.git"
                        //sshPut remote: remote, from: 'Dockerfile', into: 'root'
                        sshCommand remote: remote, command: 'docker build -t nginx-docker-jenkins patiwat13/.'
                        //sshCommand remote: remote, command: 'rm -rf  nginx-say/'
                        //sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'docker tag nginx-docker-jenkins liquid07/nginx-docker-demo:jenkins-nginx'
                        sshCommand remote: remote, command: 'docker image list'                        
                        //sshCommand remote: remote, command: 'ls -la'
                        //sshRemove remote: remote, path: "Dockerfile"
               
                  stage("Docker Login && Push"){
                        
                    sshCommand remote: remote, command: 'cp patiwat13/docker-login.sh .'
                    sshCommand remote: remote, command: 'docker push liquid07/nginx-docker-demo:jenkins-nginx'
                    echo 'Docker Push Success..!'
                    sshCommand remote: remote, command: 'rm docker-login.sh'
                        
                  }

                    stage("Git Clone"){
      
                     steps {
                           script {
                                git credentialsId: 'GIT_HUB', url: 'https://github.com/patiwat13/patiwat13.git'
                                echo 'Git Complete...'
                                sh 'pwd'
                                sh 'ls'
                                   }
                            }
                    }
                   
                   stage("Check Command Kubectl"){

            
                      sshCommand remote: remote, command: 'kubectl'
                                                    }
                   
                   stage('Copyfile in Local')
                   
                      sshCommand remote: remote, command: 'cp patiwat13/*.sh .'  //copy exportfile
                      sshCommand remote: remote, command: 'cp patiwat13/*.cfg .' //copy kubeconfig
                      sshCommand remote: remote, command: 'cp patiwat13/*.yaml .' //copy yaml
                      sshCommand remote: remote, command: 'ls'
                   
                   stage("Copy Kubeconfig On Git On VM") 
                   
                                         
                       sshCommand remote: remote, command: 'source ./export.sh && kubectl get node' + '&& kubectl cluster-info'
                       //sshCommand remote: remote, command: 'export KUBECONFIG=kubeconfig-rancher.cfg'
                       //sshCommand remote: remote, command: "pwd"
                       //sshCommand remote: remote, command: "ip a"
                       //sshCommand remote: remote, command: 'kubectl cluster-info'
                   
                   stage('Kubectl Apply Application')
                                                              
                        sshCommand remote: remote, command: 'ls' //show path
                        sshCommand remote: remote, command: 'source ./export.sh && kubectl apply -f *.yaml'
                        echo 'Kubectl Apply Success..!!'
                   
                   stage('Remove File Clone')
                   
                   
                         sshCommand remote: remote, command: 'rm -rf kubeconfig-rancher.cfg k8s-nginx-deployment.yaml patiwat13/ *.sh'
                         echo 'Remove file Success..!!'
                   
                
                  }
               }
        }
    }
        
     
                   
  
    }//steps

}//pipeline
