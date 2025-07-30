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
                        ssh -o StrictHostKeyChecking=no ubuntu@<EC2_PUBLIC_IP> "sudo rm -rf /var/www/html/*"
                        scp -o StrictHostKeyChecking=no -r * ubuntu@<EC2_PUBLIC_IP>:/var/www/html/
                        ssh -o StrictHostKeyChecking=no ubuntu@<EC2_PUBLIC_IP> "sudo systemctl restart nginx"
                    '''
                }
            }
        }
    }
}
