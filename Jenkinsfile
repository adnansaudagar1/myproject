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
                    // Step 1: Remote EC2 folder clear
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.204.66.41 "sudo rm -rf /var/www/html/*"'

                    // Step 2: Copy project files to EC2
                    sh 'scp -o StrictHostKeyChecking=no -r * ubuntu@13.204.66.41:/var/www/html/'

                    // Step 3: Restart nginx
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.204.66.41 "sudo systemctl restart nginx"'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    def response = sh(script: "curl -s -o /dev/null -w '%{http_code}' http://13.204.66.41", returnStdout: true).trim()
                    if (response == '200') {
                        echo "✅ Deployment successful! Nginx is serving content."
                    } else {
                        error "❌ Deployment failed! HTTP Status: ${response}"
                    }
                }
            }
        }
    }
}
