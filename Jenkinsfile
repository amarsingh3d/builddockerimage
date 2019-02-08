def ddockeruser = "amarsingh3d"
def imagename = "ubuntu:16"
def container = "apache2"
node {
   echo 'Building Apache Docker Image'

stage('Git Checkout') {
    git 'https://github.com/amarsingh3d/builddockerimage'
    }
    
stage('Build Docker Imagae'){
     sh label: '', script: "sudo docker build -t ${imagename} ."
    }

stage('Stop Existing Container'){
     sh label: '', script: "sudo docker stop ${container}"
    }	
	
stage ('Runing Container to test built Docker Image'){
    sh label: '', script: "sudo docker run -dit --rm --name ${container} -p 80:80 ${imagename}"
    }
    
stage('Tag Docker Image'){
    sh label: '', script: "sudo docker tag ${imagename} ${env.dockeruser}/ubuntu:16.04"
    }

stage('Docker Login and Push  Image'){
    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'dockerpasswd', usernameVariable: 'dockeruser')]) {
    sh label: '', script: "sudo docker login -u ${dockeruser} -p ${dockerpasswd}"
    }
    sh label: '', script: "sudo docker push  ${dockeruser}/ubuntu:16.04"
    }

}
