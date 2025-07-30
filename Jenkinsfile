pipeline {
    agent any
    
    stages {
        stage('Pull Code') {
            steps {
                // ✅ Correct GitHub repo URL
                git 'https://github.com/adnansaudagar1/myproject.git'
            }
        }
        
        stage('Deploy to Web Server') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'web-server',
                        transfers: [
                            sshTransfer(
                                sourceFiles: '**/*',
                                removePrefix: '',
                                remoteDirectory: '/var/www/html',
                                execCommand: 'sudo systemctl restart apache2'
                            )
                        ],
                        verbose: true
                    )
                ])
            }
        }
    }
}

