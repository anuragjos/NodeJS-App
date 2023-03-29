pipeline{
    agent any
    environment{
        DOCKERHUB_USERNAME = "anuragjoshi01"
        APP_NAME = "NodeJS-App"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = "dockerhub"
    }
    stages{
        stage("Checkout from SCM"){
            steps{
                script{
                    git credentialsId: 'github',
                    url: 'https://github.com/anuragjos/NodeJS-App.git',
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

    }




}
