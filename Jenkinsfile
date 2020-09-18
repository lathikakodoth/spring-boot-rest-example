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
	              sh "docker build -t casestudy.jfrog.io/my-docker-repo/lathika/spring-boot-rest:latest . "
}
           }
    }
   		stage ('Push image to Artifactory') {

	     agent {
                docker {
                  image 'openjdk:11.0.7'
                 }
		}
            steps {
                rtDockerPush(
                    serverId: "art-1",
                    image: "casestudy.jfrog.io/artifactory/my-docker-repo/lathika/spring-boot-rest:latest",
                    targetRepo: 'my-docker-repo',
                    properties: 'project-name=docker1;status=stable'
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "art-1"
                )
            }
        } 
}
}
