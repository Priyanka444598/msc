pipeline {
agent any

environment {
 DOCKER_BFLASK_IMAGE = 'priyanka564/myjava1:latest' // Your Docker image tag
 DOCKER_REGISTRY_CREDS = '' // Your credentials ID
}

stages {
stage('Build') {
steps {
bat 'docker build -t myjava1 .'
bat 'docker tag myjava1 %DOCKER_BFLASK_IMAGE%'
}
}

stage('Test') {
steps {
bat 'docker run --rm myjava1'
}
}

stage('Deploy') {
steps {
withCredentials([
usernamePassword(
credentialsId: "ab6f86f7-2051-4855-97a5-035dfb72f48a",
usernameVariable: 'DOCKER_USERNAME',
passwordVariable: 'DOCKER_PASSWORD'
)
]) {
bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin docker.io'
bat 'docker push %DOCKER_BFLASK_IMAGE%'
}
}
}
}

post {
always {
bat 'docker logout'
}
}
}
