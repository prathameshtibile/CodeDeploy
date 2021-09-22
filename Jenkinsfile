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

                rsync -avz -e ''ssh -i /var/lib/jenkins/backend.pem '' /var/lib/jenkins/workspace/chat-pipeline ec2-user@10.0.2.70:/home/ec2-user
               //sh 'ssh -i /var/lib/jenkins/public_instance_key.pem ubuntu@10.0.1.10 "bash /home/ubuntu/chatapp/script/Before_inst.sh"'
               //sh 'ssh -i /var/lib/jenkins/public_instance_key.pem ubuntu@10.0.1.10 "bash /home/ubuntu/chatapp/script/move.sh"'

               }
        }
        stage('Deploy') {
            steps {
               sh 'ssh -i /var/lib/jenkins/backend.pem ec2-user@10.0.2.70 "bash /home/ec2-user/chatapp/"'

            }
        }
    }
}
