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
				
					sh "ansible-playbook /var/lib/jenkins/workspace/sample/play1.yaml"
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
            
                    

                    
					
			}
		}
     }   
    }
}
