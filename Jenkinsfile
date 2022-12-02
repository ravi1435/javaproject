pipeline{
    agent any
    environment{
        PATH = "/opt/maven3.8/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
             git credentialsId: 'gitaccess', url: 'https://github.com/ravi1435/javaproject.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
            }
        }
    }
}
