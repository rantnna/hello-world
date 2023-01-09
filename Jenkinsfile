pipeline{
    agent any
    environment{
        PATH="/opt/maven/apache-maven-3.8.6/bin:$PATH"
    }
    stages{
        stage('gitcheckout'){
            steps{
                git credentialsId: 'git_cred', url: 'https://github.com/rantnna/hello-world.git'
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('deploy'){
            steps{
                sshagent(['deploy_user']) {
                sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.13.101:/opt/apache-tomcat-8.5.84/webapps"
                }
            }
        }
    }
}