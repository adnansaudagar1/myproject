
pipeline {
    agent any
    
    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/<your-username>/<repo-name>.git'
            }
        }
        
        stage('Deploy to Web Server') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'web-server', // Jenkins SSH server config ka naam
                        transfers: [
                            sshTransfer(
                                sourceFiles: 'index.html',
                                removePrefix: '',
                                remoteDirectory: '',
                                execCommand: 'sudo systemctl restart apache2'
                            )
                        ],
                        usePromotionTimestamp: false,
                        verbose: true
                    )
                ])
            }
        }
    }
}
