pipeline {
    agent any
    environment {
        PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/chaturkurma/hello-world.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install package"
            }
        }
	 
        stage('Publishing Artifact')
			{ 
			steps{
				script {
				
					sh "ansible-playbook /etc/ansible/play1.yml -i hosts -l server"
				}
			}                
		}
	 stage("deploying to Tomcat") {
			steps {
				script {
					def remote = [:]
                    remote.name = 'tomcat2'
                    remote.host = '3.84.73.92'
                    remote.user = 'ec2-user'
                    remote.password = 'Srinivyas@31'
                    remote.allowAnyHosts = true
  
                    sshCommand remote: remote, command: "/apache-tomcat-9.0.37/bin/startup.sh"
            
                    sshCommand remote: remote, command: " cd /home/ec2-user/"
                    sshCommand remote: remote, command: "sudo mv `ls -rt /home/ec2-user/*.war | tail -1` /home/ec2-user/webapp.war"
                    sshCommand remote: remote, command: "sudo cp `ls -rt /home/ec2-user/webapp.war | tail -1` /apache-tomcat-9.0.37/webapps/"
                    sshCommand remote: remote, command: "sudo rm -rf /home/ec2-user/*.war"

                    
			}
		}
     }   
    }
}
