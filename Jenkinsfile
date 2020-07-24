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
	    
	 stage("publish to nexus") {
            steps {
                script {
			nexusArtifactUploader artifacts: [[artifactId: 'maven-project', classifier: '', file: 'target/webapp.war', type: 'war']], credentialsId: 'oooo', groupId: 'com.example.maven-project', nexusUrl: '3.80.165.251:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
                }
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
  
                    sshCommand remote: remote, command: "bash /apache-tomcat-9.0.37/bin/startup.sh"
            
                    

                    
					
			}
		}
     }   
    }
}
