pipeline {
    agent any

    stages {
        stage('Git  Clone') {
            steps {
                git  'https://github.com/prathameshtibile/CodeDeploy.git '
            }
        }

        stage('Build') {
            steps {
                sh 'rsync -avz -e 'ssh -i ec2-user@10.0.2.70 /var/lib/jenkins/backend.pem' /var/lib/jenkins/workspace/chat-pipeline:~/'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ssh -i /var/lib/jenkins/backend.pem ec2-user@10.0.2.70 "bash /var/lib/jenkins/workspace/chat-pipeline/jen.sh/"'
              
            }
        }
    }
}
