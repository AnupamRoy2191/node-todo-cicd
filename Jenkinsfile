pipeline {
    agent { label "test" }
	environment {
		DOCKERHUB_CREDS=credentials('dockerHub')
	}
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/AnupamRoy2191/node-todo-cicd.git", branch: "main"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t $DOCKERHUB_CREDS_USR/node-app-test-new:latest"
           	 }
        }
        stage("Push to Docker Hub"){
            steps{
                sh "docker login -u $DOCKERHUB_CREDS_USR -p '$DOCKERHUB_CREDS_PSW'"
                sh "docker push $DOCKERHUB_CREDS_USR/node-app-test-new:latest"
                }
            }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
