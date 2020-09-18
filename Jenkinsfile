pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    environment {
    PATH = "/usr/bin:$PATH"
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
		docker.build  "lathika/spring-boot-rest:latest"
}
           }
    }
  }
    
}
