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
                 
                 echo 'SSH Success'
                 
                 stage('Using Command') {
                        sshCommand remote: remote, command: "pwd"
                        sshCommand remote: remote, command: "whoami"
                        sshCommand remote: remote, command: "docker version"
                        sshCommand remote: remote, command: 'docker build -t nginx-docker-jenkins .'
                        sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'docker tag nginx-docker-demo liquid07/nginx-docker-demo:jenkins-nginx'
                        sshCommand remote: remote, command: 'docker image list'
                        sshPut remote: remote, from: 'Dockerfile', into: '.'
                        sshRemove remote: remote, path: "Dockerfile"
      }
     
                     }
    
              }
       
     }
  }
  
}
