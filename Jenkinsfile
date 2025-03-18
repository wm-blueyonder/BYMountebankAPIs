pipeline {
    agent any
	
	     environment{
                    remoteHost = ' 172.31.9.115'
                    remotePath = '/data/bymountebank/BYMountebankAPIs'
					containerName = 'BYmountebank'
}
    stages {
        stage('Copy to Remote Host and Deploy ') {
            steps {
                script {
               
                    // SSH into the remote host
                    sshagent(['prod-deployment-ssh-details']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${env.remoteHost}"
						//copy and overwrite the files
                        sh "scp -r /var/jenkins_home/workspace/BYmountebank/* ubuntu@${env.remoteHost}:${env.remotePath}"

                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${env.remoteHost} 'docker restart ${env.containerName}' "
                    }
                }
            }
        }

        
    }
}
