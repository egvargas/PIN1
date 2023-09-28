pipeline {
    agent any

    options {
        timeout(time: 2, unit: 'MINUTES')
    }

    stages {
        stage('Building image') {
            steps {
                sh '''
                docker build -t egvargas/pin1 .
                '''  
            }
        }

        stage('Run tests') {
            steps {
                sh '''
                docker run pin1:latest npm test 
                '''
                    }
                }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                        sh "docker push egvargas/tpi1"
                    }
                }
            }
        }
    }
}


    
  

