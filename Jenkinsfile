node{
	stage('SCM Checkout'){
		git branch: 'wartomcat', url: 'https://github.com/care2manoj/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'mymaven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['pem-tomcat']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@54.174.38.159:/opt/tomcat9/webapps/'
	}
	}
	
}
