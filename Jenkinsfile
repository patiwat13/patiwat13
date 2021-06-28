pipeline {
  agent any
  
  stages{
     
    stage("Git Clone"){
      
                     steps {
                           script {
                                git credentialsId: 'GIT_HUB', url: 'https://github.com/patiwat13/nginx-say.git'
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
                        sshCommand remote: remote, command: "git clone https://github.com/patiwat13/nginx-say.git"
                        //sshPut remote: remote, from: 'Dockerfile', into: 'root'
                        sshCommand remote: remote, command: 'docker build -t nginx-docker-jenkins nginx-say/.'
                        //sshCommand remote: remote, command: 'rm -rf  nginx-say/'
                        sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'docker tag nginx-docker-jenkins liquid07/nginx-docker-demo:jenkins-nginx'
                        sshCommand remote: remote, command: 'docker image list'
                        sshCommand remote: remote, command: 'cd nginx-say/'
                        sshCommand remote: remote, command: 'ls -la'
                        //sshRemove remote: remote, path: "Dockerfile"
                
                  
                   
                   
      }
                 stage("Git Clone"){
      
                     steps {
                           script {
                              
                             sh 'pwd'
                             
                           }
                     }
                 }
                 
                 stage("Login to Rancher"){ 
                    
                    steps {
               script {
      kubeconfig(caCertificate: '''-----BEGIN CERTIFICATE-----
MIIBiDCCAS6gAwIBAgIBADAKBggqhkjOPQQDAjA7MRwwGgYDVQQKExNkeW5hbWlj
bGlzdGVuZXItb3JnMRswGQYDVQQDExJkeW5hbWljbGlzdGVuZXItY2EwHhcNMjEw
MzI0MDUwNzA2WhcNMzEwMzIyMDUwNzA2WjA7MRwwGgYDVQQKExNkeW5hbWljbGlz
dGVuZXItb3JnMRswGQYDVQQDExJkeW5hbWljbGlzdGVuZXItY2EwWTATBgcqhkjO
PQIBBggqhkjOPQMBBwNCAARMO7Ag8armJKKvhRcxCsHp1+oWwLiHoY7krAeOjVca
hzXGQu5zaAQyRvgvE8TElXvTVJV6GuFUpAfMqCcA/k8YoyMwITAOBgNVHQ8BAf8E
BAMCAqQwDwYDVR0TAQH/BAUwAwEB/zAKBggqhkjOPQQDAgNIADBFAiEA6cmHVpNu
1oURR8FBKm46uldAVG8/iqed05X5Ob0VXXQCIDpXcbQUussfetNfmHb65hwc/2tW
P9V/xvyOokeKAvZd
-----END CERTIFICATE-----''', credentialsId: 'Rancher_Login', serverUrl: 'https://203.151.50.20/k8s/clusters/c-bfhk6') {
    // some block
            stage('Deploy Nginx YAML File') {
              
                  echo 'kubeconfig'
                  //sh 'kubectl apply -f nginx-deployment.yaml'
                  // sh 'kubectl get pod'
                                    }
      }
               }

    }
                                }
     
                     }
    
              }
       
     }
  }
  
}
