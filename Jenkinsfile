pipeline {
    agent {
    label {
        label "built-in"
        customWorkspace "/project/"
        }
    }
    stages {
        stage ("Cloning") {
            steps {
                cleanWs()
                /*git credentialsId: 'lokesh', url: 'https://github.com/kiran064/Myproject.git'*/
		git 'https://github.com/kiran064/Myproject.git'
            }
        }
        stage ("Build") {
            steps {
                sh "mvn clean install"
            }
        }
        stage ("Copy") {
            steps {
                stash includes: 'target/*.war', name: 'project'
            }
        }
        stage ("Deploy"){
		agent {
		node {
				label "Linux"
		}
		}
		steps {
		    unstash 'project'
		    sh "sudo cp -r /home/ec2-user/workspace/DeployUsringStash/target/vprofile-v2.war /tom/apache-tomcat-9.0.70/webapps/"
		}
		}
    }
}
