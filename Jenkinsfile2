pipeline {
    agent {
        docker {
            image 'docker'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
	stage('build') {
            steps {
        sh 'docker build -t lathika/spring-boot-rest:latest .'
    }
}
}
}
