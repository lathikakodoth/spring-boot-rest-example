pipeline {
    agent none
    stages {
	
        stage('Maven Install') { 
	    
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
	 stage('Docker Build') {
	     agent {
                docker {
                  image 'docker'
                  args '-v /var/run/docker.sock:/var/run/docker.sock'
                 }
               } 
            steps {
                script {
	              sh "docker build -t lathika/spring-boot-rest:latest . "
}
           }
    }
  }
    
}
