node{
	stage('SCM Checkout'){
		git branch: 'wartomcat', url: 'https://github.com/care2manoj/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'mymaven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['ppk-tomcat']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.173.144.248:/opt/tomcat9/webapps/'
	}
	}
	
}
