pipeline {
    agent any

    parameters {
        string(name: 'SERVICE_NAME', defaultValue: '', description: 'Name of the service directory')
        string(name: 'IMAGE_FULL_NAME_PARAM', defaultValue: '', description: 'New image full name parameter')
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    // Change directory to the SERVICE_NAME directory
                    dir('NetflixFrontend') {
                        // Change YAML manifests according to IMAGE_FULL_NAME_PARAM
                        sh "sed -i 's/image/$IMAGE_FULL_NAME_PARAM/g' file.yaml"

                        // Commit the changes and push to GitHub
                        sh """
                        git config --global user.name "Your Name"
                        git config --global user.email "your.email@example.com"
                        git add .
                        git commit -m "Update image reference in YAML file"
                        git push
                        """
                    }
                }
            }
        }
    }
}
    }
}