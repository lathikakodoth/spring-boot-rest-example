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
	stage('Docker Push') {
      	     agent {
                docker {
                  image 'docker'
                  args '-v /var/run/docker.sock:/var/run/docker.sock'
                 }
               } 
      
steps {
        withCredentials([usernamePassword(credentialsId: 'artifactory', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
          sh 'docker push lathika/spring-boot-rest:latest'
        }
      }
    }
  }
    
}
