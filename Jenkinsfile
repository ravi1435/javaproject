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
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy-dev"){
             sshagent(['tomcat-new']) {
                   sh """
                       scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@172.31.30.138:/opt/tomcat8/webapps/
                    
                       ssh ec2-user@172.31.30.138 /opt/tomcat8/bin/shutdown.sh
                    
                       ssh ec2-user@172.31.30.138 /opt/tomcat8/bin/startup.sh
                   """
             }
        }
    }
}
