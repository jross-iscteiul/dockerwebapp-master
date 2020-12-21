pipeline {
    agent { label: "default" }
    stages {
       
        stage('Deploy Production') {
            steps{
			 checkout scm
	
    docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {

        def customImage = docker.build("sksuricata/dockerwebapp")

        /* Push the container to the custom Registry */
        customImage.push()
                git url: 'https://github.com/jross-iscteiul/dockerwebapp-master'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "my-project-id",
                        clusterName: "production",
                        zone: "us-central1-f",
                        manifestPattern: 'k8s/production/',
                        credentialsId: "gke-service-account",
                        verifyDeployments: true])
            }
        }
    }
}