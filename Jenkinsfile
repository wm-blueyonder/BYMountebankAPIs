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
                    sshagent(['salesbot deployment key']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${env.remoteHost}"
						//copy and overwrite the files
                        sh "scp -r /var/jenkins_home/workspace/att-mvno/mvno_mountebank/* ubuntu@${env.remoteHost}:${env.remotePath}"

                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${env.remoteHost} 'docker restart ${env.containerName}' "
                    }
                }
            }
        }

        
    }
}
