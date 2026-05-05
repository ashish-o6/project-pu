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

	stage('Push to Dockerhub'){
	   steps {
	   	sh 'docker push ashish3507/my-node-app'
		}
	}

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:3000 ashish3507/my-node-app'
            }
        }
    }
}
