pipeline {
    agent any
    
    environment {
        DOCKER_HUB_USER = 'jatink9599' 
        IMAGE_NAME = 'autodeployx'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/jatinkapoor009/autodeployx.git', branch: 'main'
            }
        }

        stage('Build & Tag Image') {
            steps {
                sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:${env.BUILD_NUMBER} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-token-new', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh "echo \$DOCKER_HUB_PASSWORD | docker login -u \$DOCKER_HUB_USERNAME --password-stdin"
                    sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
                    sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:${env.BUILD_NUMBER}"
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                sh "docker rm -f autodeployx-staging || true"
                sh "docker run -d -p 8081:80 --name autodeployx-staging ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
            }
        }

        stage('Manual Approval') {
            steps {
                timeout(time: 2, unit: 'HOURS') {
                    input message: 'Staging (8081) check kar liya? Production (80) update karein?', ok: 'Deploy Now'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                sh "docker rm -f autodeployx-container || true"
                sh "docker run -d -p 80:80 --name autodeployx-container ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            mail to: 'jatink9599@gmail.com',
                 subject: "Success: Build #${env.BUILD_NUMBER} of ${env.JOB_NAME}",
                 body: "Bhai, Mubarak ho! Pipeline successfully khatam ho gayi hai.\nBuild Number: ${env.BUILD_NUMBER}\nCheck yahan karo: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'jatink9599@gmail.com',
                 subject: "Failure: Build #${env.BUILD_NUMBER} of ${env.JOB_NAME}",
                 body: "Oops! Build fail ho gayi hai. Jaldi check karo kya hua: ${env.BUILD_URL}console"
        }
    }

