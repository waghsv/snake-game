pipeline {
    agent any
     environment {
        AWS_ACCOUNT_ID = "339712822600"
        AWS_DEFAULT_REGION = "ap-south-1"
        IMAGENAME = "snake-game"
        IMAGE_REPO_NAME = "projectrepo1"
        IMAGE_TAG = "latest"

    //    // AWS_ACCOUNT_ID="CHANGE_ME"
    //    // AWS_DEFAULT_REGION="CHANGE_ME" 
	//     CLUSTER_NAME="Node-app"
	//     SERVICE_NAME="node-service"
	//     TASK_DEFINITION_NAME="Node-fam"
    // 	DESIRED_COUNT="2"
    //     REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
        
    // }
    
    stages {

        // stage('Logging into AWS ECR') {
        //     steps {
        //         script {
        //             sh """aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"""
        //         }  
        //     }
        // }
        
        stage("code"){
            steps{
                git url: "https://github.com/waghsv/snake-game.git", branch: "master"
                echo 'Print the output'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t snake-game"
                echo 'print the output'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }

        stage('Pushing to ECR') {
            steps {  
                script {
                    sh """docker tag ${IMAGENAME}:${IMAGE_TAG} ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"""
                    sh """docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"""
                }
            }
        }
        // stage('Ecr Deploy'){
        //     steps{
        //           script {
        //             sh """chmod +x script.sh"""
		// 	        sh './script.sh'
        //         }
        //     }
        // }

        // stage("push"){
        //     steps{
        //         withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
        //         sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
        //         sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
        //         sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
        //         echo 'image push ho gaya'
        //         }
        //     }
        // }
        // stage("deploy"){
        //     steps{
        //         sh "docker-compose down && docker-compose up -d"
        //         echo 'deployment ho gayi'
        //     }
        // }
    }
}