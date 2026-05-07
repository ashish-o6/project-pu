pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/ashish-o6/project-pu.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }
	
	stage('Tag Image'){
	    steps {
	    	sh 'docker tag my-node-app ashish3507/my-node-app'
	    	}
	}

	stage('Push to Dockerhub') {
    	   steps {
        	withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
            	sh '''echo $PASS | docker login -u $USER --password-stdin docker push ashish3507/my-node-app'''
                }
    	    }	
	}

       stage('Run Container') {
    	  steps {
        	sh 'docker rm -f my-container || true'
        	sh 'docker run -d -p 3000:3000 --name my-container ashish3507/my-node-app'
    	  }	
       }
    }
}
