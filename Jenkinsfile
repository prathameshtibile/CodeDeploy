pipeline {
    agent any

    stages {
        stage('Git  Clone') {
            steps {
                git  'https://github.com/prathameshtibile/CodeDeploy.git '
            }
        }

        stage('sonarqube') {
            environment {
                scannerHome = tool 'sonarqubescanner'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                    -Dsonar.login=admin \
                    -Dsonar.password=Pass@9858 \
                    -Dsonar.projectKey=sonarproject \
                    -Dsonar.sources=src/main/java/
                    -Dsonar.exclusions=vendor/**,resources/**,**/*.java \
                    -Dsonar.host.url=http://3.143.213.97:9000/
                    
                    
                }
//                 timeout(time: 10, unit: 'MINUTES') {
//                     waitForQualityGate abortPipeline: true
//                 }
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
