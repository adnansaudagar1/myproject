pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/adnansaudagar1/myproject.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no -r * ubuntu@<EC2-Public-IP>:/usr/share/nginx/html/
                        ssh -o StrictHostKeyChecking=no ubuntu@<EC2-Public-IP> "sudo systemctl restart nginx"
                    '''
                }
            }
        }
    }
}



