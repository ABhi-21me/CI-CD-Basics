node {
    stage('Build image') {
        sh 'docker build -f DOCKERFILE -t abhiv21/mywebsite:latest .'
    }

    stage('Push to DockerHub') {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                                          usernameVariable: 'DH_USER',
                                          passwordVariable: 'DH_PASS')]) {
            sh 'echo "$DH_PASS" | docker login -u "$DH_USER" --password-stdin'
            sh 'docker push abhiv21/mywebsite:latest'
        }
    }

    stage('Run container') {
        sh 'docker rm -f mywebsite || true'
        sh 'docker run -d -p 8081:80 --name mywebsite abhiv21/mywebsite:latest'
    }
}