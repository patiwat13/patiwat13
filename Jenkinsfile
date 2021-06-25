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
      }
     
                     }
    
              }
       
     }
  }
  
}
