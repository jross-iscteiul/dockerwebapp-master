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
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud init'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud config set account jenkins@agisit0.iam.gserviceaccount.com	'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud auth activate-service-account jenkins@agisit0.iam.gserviceaccount.com --key-file=/home/ec2-user/agisit0-044fdfc139a2.json --project=agisit0 --verbosity=debug --quiet'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud config set project agisit0'
			sh' sudo /home/ec2-user/google-cloud-sdk/bin/gcloud container clusters get-credentials ci-cd-cluster  --zone=europe-west1-b'
			sh 'sudo /home/ec2-user/google-cloud-sdk/bin/gcloud container clusters describe ci-cd-cluster --zone=europe-west1-b' 
			sh 'sudo kubectl config view'
			int status = sh(script: """ sudo kubectl get deployment docker-web-app """ , returnStatus: true)
			if(status==0){
			sh 'sudo kubectl set image deployment docker-web-app dockerwebapp=sksuricata/dockerwebapp:latest'
			sh 'sudo kubectl describe deployment docker-web-app'
			}else{
			sh 'sudo kubectl create deployment --image=sksuricata/dockerwebapp:latest docker-web-app '
			sh 'sudo kubectl set env deployment.apps/docker-web-app DOMAIN=cluster'
			sh "sudo kubectl get pods"
			}
				
			}}
		}
		
		stage('Set services Kube'){
			steps{
			script {
			if(status!=0){
			sh 'sudo kubectl expose deployment docker-web-app --name=docker-web-app-service --type=LoadBalancer --port 8090 --target-port 8080  '
			}
			sh 'sudo kubectl get service'
			}
		}
	
	
	}
	}
	



}
