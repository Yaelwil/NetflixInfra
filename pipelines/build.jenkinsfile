pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_FULL_NAME', defaultValue: '', description: 'Full name of the Docker image built')
    }

    stages {
        stage('Build') {
            steps {
                // Build Docker image steps
                sh "docker build -t $IMAGE_FULL_NAME ."
                // Push Docker image steps
                sh "docker push $IMAGE_FULL_NAME"
            }
        }

        stage('Trigger Deploy') {
            steps {
                build job: 'NetflixFrontendDeploy', wait: false, parameters: [
                    string(name: 'SERVICE_NAME', value: 'NetflixFrontend'),
                    string(name: 'IMAGE_FULL_NAME_PARAM', value: "${params.IMAGE_FULL_NAME}")
                ]
            }
        }
    }
}
