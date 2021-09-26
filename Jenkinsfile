pipeline {
    agent any

    stages {
        stage('Git  Clone') {
            steps {
                git  'https://github.com/prathameshtibile/CodeDeploy.git '
            }
        }

        stage ('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sonarqube') {
                    sh 'mvn clean package sonar:sonar'
                }
            }    
        }
        
        stage('Build') {
            steps {
                sh 'rsync -avz -e "ssh -i /var/lib/jenkins/backend.pem" /var/lib/jenkins/workspace/chat-pipeline ec2-user@10.0.2.70:~/'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ssh -i /var/lib/jenkins/backend.pem ec2-user@10.0.2.70 "bash /home/ec2-user/chat-pipeline/jen.sh"'

            }
        }
    }
}

