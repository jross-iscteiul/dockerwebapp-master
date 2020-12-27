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
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud config set account jenkins@agisit0.iam.gserviceaccount.com	'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud auth activate-service-account jenkins@agisit0.iam.gserviceaccount.com --key-file=/home/ec2-user/agisit0-044fdfc139a2.json --project=agisit0 --verbosity=debug --quiet'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud config set project agistit0'
			sh' sudo /home/ec2-user/google-cloud-sdk/bin/gcloud container clusters get-credentials ci-cd-cluster  --zone=europe-west1-b'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud container clusters describe ci-cd-cluster --zone=europe-west1-b' 
			sh 'sudo kubectl config view'
		
			sh 'kubectl create deployment --image=sksuricata/dockerwebapp:latest v0'
			sh 'kubectl set env deployment.apps/v0 DOMAIN=cluster'
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
