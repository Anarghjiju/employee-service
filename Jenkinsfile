pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Anarghjiju/employee-service.git.git', branch: 'main'
            }
        }
        stage('Pre_Build'){
            steps {
                bat "docker rm -f emp_container"
                bat "docker rmi -f emp_image"
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {

                bat "docker build -t emp_image ."
                bat "docker run -p 8082:8082 -d --name emp_container emp_image"
            }
        }
    }
}
