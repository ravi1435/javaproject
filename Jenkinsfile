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
                sh "mv target/*.war target/javaproject.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@172.31.30.138:/home/ec2-user/apache-tomcat-9.0.64/webapps/
                    
                    ssh ec2-user@172.31.30.138 /home/ec2-user/apache-tomcat-9.0.64/bin/shutdown.sh
                    
                    ssh ec2-user@172.31.30.138/home/ec2-user/apache-tomcat-9.0.64/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
