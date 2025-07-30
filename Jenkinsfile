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
                        ssh -o StrictHostKeyChecking=no ubuntu@<13.204.66.41> "sudo rm -rf /var/www/html/*"
                        scp -o StrictHostKeyChecking=no -r * ubuntu@<13.204.66.41>:/var/www/html/
                        ssh -o StrictHostKeyChecking=no ubuntu@<13.204.66.41> "sudo systemctl restart nginx"
                    '''
                }
            }
        }
    }
}
