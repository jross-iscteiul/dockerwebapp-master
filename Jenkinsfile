pipeline {
    agent any
	environment {
        PROJECT_ID = 'AGISIT0'
        CLUSTER_NAME = 'ci-cd-cluster'
        LOCATION = 'europe-west1-b'
        CREDENTIALS_ID = 'GKE_Caps'
    }
    stages {
       
         stage('Deploy to GKE') {
            steps{
                step([
                $class: 'KubernetesEngineBuilder',
                projectId: env.PROJECT_ID,
                clusterName: env.CLUSTER_NAME,
                location: env.LOCATION,
                manifestPattern: 'manifest.yaml',
                credentialsId: env.CREDENTIALS_ID,
                verifyDeployments: true])
            }
        }
    }
}
