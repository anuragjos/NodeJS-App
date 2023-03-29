pipeline{
    agent any
    environment{
        DOCKERHUB_USERNAME = "anuragjoshi01"
        APP_NAME = "nodejs-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = "dockerhub"
    }
    stages{
        stage("Checkout from SCM"){
            steps{
                script{
                    git credentialsId: 'github',
                    url: 'https://github.com/anuragjos/nodejs-app.git',
                    branch: 'main'

                }
            }
        }
        stage("Docker Build Image"){
            steps{
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage("Docker Image Push to Docker Hub"){
            steps{
                script{
                    docker.withRegistry('',REGISTRY_CREDS){
                    docker_image.push("$BUILD_NUMBER")
                    docker_image.push ('latest')
                    }
                }
            }
        }
        stage("Deleting Docker Images"){
            steps{
                script{
                    sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                    sh "docker rmi ${IMAGE_NAME}:latest"
                }
            }
        }

    }




}
