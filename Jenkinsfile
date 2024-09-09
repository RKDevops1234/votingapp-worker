pipeline {
    agent any

    environment {
        VERSION = '1'
    }

    stages {
        stage('Build-worker') {
            steps {
                // Checkout the code
                git branch: 'main',
                    credentialsId: 'github',
                    url: 'https://github.com/RKDevops1234/votingapp-worker.git'

                // Print the Git repository information
                sh 'git remote -v'
                sh 'git branch -a'
                sh 'git status'

                // Build the Docker image
                sh "docker build -t rajeshtalla0209/votingapp-worker:${VERSION} ."
            }
        }

        stage('Run-wroker') {
            steps {
                // Run the Docker container and expose port 80
                sh "docker run -p 80:80 -d rajeshtalla0209/votingapp-worker:${VERSION}"
            }
        }

        stage('Push to Docker Hub - worker') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_TOKEN', variable: 'DOCKER_HUB_TOKEN')]) {
                    // Log in to Docker Hub using a token
                    sh "echo ${DOCKER_HUB_TOKEN} | docker login -u rajeshtalla0209 --password-stdin https://registry.hub.docker.com"

                    // Tag the image with your Docker Hub username and repository name
                    sh "docker tag rajeshtalla0209/votingapp-worker:${VERSION} rajeshtalla0209/votingapp-worker:${VERSION}"

                    // Push the image to Docker Hub
                    sh "docker push rajeshtalla0209/votingapp-worker:${VERSION}"
                }
            }
        }
    }
}
// Initial  one 