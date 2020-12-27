pipeline{

    agent { node { label 'master' } }

	stages{
		
		stage('checkout') {
			steps{
				checkout scm
		}
	}
		stage('Build image'){
		steps{
		script{
			
		docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {

		def customImage = docker.build("sksuricata/dockerwebapp")

        /* Push the container to the custom Registry */
        customImage.push()	
			}
			
			
		}
		}}
		stage('Deploy to Docker'){
			steps{
			sh 'echo cluster-info'
			}
		}
		
		stage('Deploy to Kube'){
			steps{
			
			script {
			sh 'echo noanananana-info'

			sh "kubectl config view"

			sh "kubectl config --kubeconfig=/home/ec2-user/jenkins/config use-context dev-frontend"
			sh "kubectl config view"
			sh "kubectl create deployment --image=sksuricata/dockerwebapp:latest v0"
			sh "kubectl set env deployment.apss/v0 DOMAIN=cluster"
			sh "kubectl get pods"
				
			}}
		}
		
		stage('Set services Kube'){
			steps{
			sh 'kubectl expose deployment v0 --name=v0-app-service --type=LoadBalancer --port 8090 --target-port 8080  '
			sh 'kubectl get service'
			}
		}
	
	
	}
	/*0bd79863a8d047c498a43b60658803782b9b1061*/



}