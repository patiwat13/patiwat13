pipeline {
  agent any
  
  stages{
     
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
    
    stage('SSH into the server') {
        steps {
               script {
                            def remote = [:]
                            remote.name = 'K8S master'
                            remote.host = '192.168.1.100'
                            remote.user = 'root'
                            remote.password = 'zjkoC]6p'
                            remote.allowAnyHosts = true
                 
                 
                 echo 'SSH Success'
                 
                 stage('Using Command') {
                        
                        //sshCommand remote: remote, command: "pwd"
                        //sshCommand remote: remote, command: "whoami"
                        sshCommand remote: remote, command: "git clone https://github.com/patiwat13/patiwat13.git"
                        //sshPut remote: remote, from: 'Dockerfile', into: 'root'
                        sshCommand remote: remote, command: 'docker build -t nginx-docker-jenkins patiwat13/.'
                        //sshCommand remote: remote, command: 'rm -rf  nginx-say/'
                        sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'docker tag nginx-docker-jenkins liquid07/nginx-docker-demo:jenkins-nginx'
                        sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'cp patiwat13/*yaml .'
                        sshCommand remote: remote, command: 'ls -la'
                        //sshRemove remote: remote, path: "Dockerfile"
                   
                   
                   stage("Check Command Kubectl"){

            
                      sshCommand remote: remote, command: 'kubectl'
                      sshCommand remote: remote, command: "whoami"
                                }
                   
                   stage("Copy Kubeconfig On Git On VM") 
                   
                       sshCommand remote: remote, command: 'cp patiwat13/*cfg .'
                       //sshCommand remote: remote, command: 'export KUBECONFIG=kubeconfig-rancher.cfg'
                       sshCommand remote: remote, command: "pwd"
                       sshCommand remote: remote, command: "whoami"
                       sshPut remote: remote, from: 'export.sh', into: '.'
                       sshCommand remote: remote, command: 'source ./export.sh && echo $KUBECONFIG'
                       sshCommand remote: remote, command: 'kubectl cluster-info'
                   
                
                  }
               }
        }
    }
        
     
                   
  
    }//steps

}//pipeline
