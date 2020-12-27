pipeline{

	agent any

	stages{
		
		stage('checkout') {
			node {
				checkout scm
				 }
	}
		stage('Build image'){
			docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {

			def customImage = docker.build("sksuricata/dockerwebapp:v0")
			/*sh 'docker build -t sksuricata/main .'*/
			customImage.push()
			
        /* Push the container to the custom Registry */
			
		}}
		
		stage('Deploy to Docker'){
			sh 'docker run -p 91:8080 sksuricata/dockerwebapp:v0'
			
		}
		
		stage('Deploy to Kube'){
			sh 'kubectl create deployment --image=sksuricata/dockerwebapp:v0 v0'
			sh 'kubectl set env deployment.apss/v0 DOMAIN=cluster'
			sh 'kubectl get pods'
			
		}
		
		stage('Set services Kube'){
			sh 'kubectl expose deployment v0 --name=v0-app-service --type=LoadBalancer --port 8090 --target-port 8080  '
			sh 'kubectl get service'
		}
	
	
	}
	/*0bd79863a8d047c498a43b60658803782b9b1061*/



}