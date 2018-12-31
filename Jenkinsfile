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
	stage('Build Docker Image'){
        sh 'docker build -t care2manoj/devopsprojects:2.0.0 .'
        
    	}
	stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DockerHubPass', variable: 'DockerHubPass')]){
            sh "docker login -u care2manoj -p ${DockerHubPass}"
    	}
        sh 'docker push care2manoj/devopsprojects:2.0.0'
    	}
	stage('Run Container on Prod Server'){
        def dockerRun = 'sudo docker run -p 8085:8080 -d care2manoj/devopsprojects:2.0.0'
        sshagent(['ppk-tomcat']) {
            sh "ssh -o StrictHostKeyChecking=no ubuntu@54.173.144.248 ${dockerRun}"
        }
    	}
	
}
