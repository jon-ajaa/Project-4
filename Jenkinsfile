pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'jonajaa/jfc:latest'
        CONTAINER_NAME = 'jfc'
        PORT_MAPPING = '8089:80'  // adjust the port mapping as needed
        AUTHOR1 = "Muhammad Azhar Najib"
        AUTHOR2 = "Gerhard Jeremia"
    }

    stages{
        stage('Environment Information'){
            steps{
                echo "Author 1:  ${AUTHOR1}"
                echo "Author 2: ${AUTHOR2}"
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Workspace: ${env.WORKSPACE}"
                echo "Node Name: ${env.NODE_NAME}"
            }
        }
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}", '-f Dockerfile .')
                }
            }
        }

    // stage('Clean Existing Container') {
    //     steps {
    //         script {
    //             bat """
    //             FOR /F "tokens=*" %%i IN ('docker ps -aq -f "name=${CONTAINER_NAME}"') DO (
    //                 docker stop %%i || echo "No running container"
    //                 docker rm %%i || echo "No container to remove"
    //             )
    //             """
    //         }
    //     }
    // }


        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container based on the built image
                    docker.image("${DOCKER_IMAGE}").run("-p ${PORT_MAPPING} --name ${CONTAINER_NAME}")
                }
            }
        }
    }
}
