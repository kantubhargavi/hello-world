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
        stage('Publishing Artifact')
			{ 
			steps{
				script {
				
					sh "ansible-playbook /etc/ansible/play1.yml"
				}
			}                
		}
    }
}
