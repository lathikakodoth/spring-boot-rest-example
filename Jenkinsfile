pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Maven Install') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
	 stage('Docker Build') {
	    agent any
            steps {
                script {
                sh 'which docker'
		sh 'printenv'
		sh 'docker build -t lathika/spring-boot-rest:latest .'
}
           }
    }
  }
    
}
