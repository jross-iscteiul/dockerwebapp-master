node {

    checkout main
	
    docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {

        def customImage = docker.build("sksuricata/dockerwebapp")

        /* Push the container to the custom Registry */
        customImage.push()
    }
}