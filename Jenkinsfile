pipeline{
    agent any
    tools{
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages{
        stage('Clone'){
            steps{
                git url:'https://github.com/ArchitAvd/service-registry',branch:'master'
            }
        }
        stage('Build'){
            steps{
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test'){
            steps{
                bat "mvn test"
            }
        }
        stage('Deploy'){
            steps{
                bat "docker rm -f my-serv-container"
                bat "docker rmi -f my-serv-image"
                bat "docker build -t my-serv-image ."
                bat "docker run -p 8761:8761 -d --name my-serv-container my-serv-image"
            }
        }
    }
}