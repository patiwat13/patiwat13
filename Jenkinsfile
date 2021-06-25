pipeline {
  agent any
  
  stages{
     stage('SSH into the server') {
        steps {
               script {
                            def remote = [:]
                            remote.name = 'K8S master'
                            remote.host = '192.168.1.100'
                            remote.user = 'root'
                            remote.password = 'zjkoC]6p'
                            remote.allowAnyHosts = true
                 
                 stage("Git Clone"){
                   
                   steps {
         git credentialsId: 'GIT_HUB', url: 'https://github.com/patiwat13/nginx-say.git'
      }
                 }
                 echo 'SSH Success'
                 
                 stage('Using Command') {
                        
                        //sshCommand remote: remote, command: "pwd"
                        //sshCommand remote: remote, command: "whoami"
                        sshCommand remote: remote, command: "git clone https://github.com/patiwat13/nginx-say.git"
                        //sshPut remote: remote, from: 'Dockerfile', into: 'root'
                        sshCommand remote: remote, command: 'docker build -t nginx-docker-jenkins nginx-say/.'
                        sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'docker tag nginx-docker-jenkins liquid07/nginx-docker-demo:jenkins-nginx'
                        sshCommand remote: remote, command: 'docker image list'
                        //sshRemove remote: remote, path: "Dockerfile"
      }
     
                     }
    
              }
       
     }
  }
  
}
