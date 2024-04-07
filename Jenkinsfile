pipeline {
    agent { label 'builder-node' }
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: '')
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    //Clone the repository using SSH with private key and checkout the specific branch
                    git credentialsId: 'jenkins-agent-node',
                        url: 'https://github.com/s8kevinaf02/web.git',
                        branch: "${params.BRANCH_NAME}"
                }
            }
        }
        stage('Install Apache') {
            steps {
                script {
                    sh """
                        sudo apt update -y
                        sudo apt install apache2 -y
                        sudo systemctl start apache2
                        sudo systemctl status apache2
                        sudo systemctl enable apache2
                    """
                }
            }
        }
        stage('Clean up html directory') {
            steps {
                script {
                    sh """
                        cd /var/www/html
                        ls -l
                        sudo rm -rf *
                        ls -l
                    """ 
                }
            }
        }
        stage('Deploying the Code') {
            steps {
                script {
                    sh """
                        pwd
                        ls -l
                        sudo cp -r * /var/www/html
                    """ 
                }
            }
        }
    }
}
