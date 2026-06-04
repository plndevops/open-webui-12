pipeline {
    agent any

    stages {

        stage('Update Code') {
            steps {
                sh '''
                cd /home/ubuntu/open-webui-12
                git pull origin main
                '''
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                sh '''
                cd /home/ubuntu/open-webui-12/backend
                /home/ubuntu/open-webui-12/venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                sh '''
                cd /home/ubuntu/open-webui-12
                npm install
                '''
            }
        }

        stage('Build Frontend') {
            steps {
                sh '''
                cd /home/ubuntu/open-webui-12
                export NODE_OPTIONS="--max-old-space-size=6144"
                npm run build
                '''
            }
        }

        stage('Restart OpenWebUI') {
            steps {
                sh '''
                sudo systemctl restart openwebui
                '''
            }
        }

        stage('Verify Service') {
            steps {
                sh '''
                sudo systemctl status openwebui --no-pager
                '''
            }
        }
    }
}
