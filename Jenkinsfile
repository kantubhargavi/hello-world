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
              sh "mvn clean install"
            }
        }
	 stage("publish to nexus") {
            steps {
                script {
				 nexusArtifactUploader artifacts: [[artifactId: 'maven-project', classifier: '', file: 'target/webapp.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.example.maven-project', nexusUrl: '3.87.139.124:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
                }
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
    }
}
