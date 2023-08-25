pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout main
            }
        }
        
        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        
        stage('Build Backend') {
            steps {
                dir('backend') {
                    sh 'python3 -m venv venv'
                    sh '. venv/bin/activate'
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        
        stage('Frontend Testing') {
            steps {
                dir('frontend') {
                    sh 'npm test'
                }
            }
        }
        
        stage('Backend Testing') {
            steps {
                dir('backend') {
                    sh 'pytest'
                }
            }
        }
        
        stage('Deployment') {
            steps {
                // Deploy frontend and backend
                // Replace the following lines with actual deployment commands
                
                // Frontend deployment (e.g., Nginx)
                sh 'sudo cp -r frontend/build/* /var/www/html/'
                
                // Backend deployment (e.g., Gunicorn)
                sh 'source backend/venv/bin/activate && gunicorn -w 4 -b 0.0.0.0:5000 app:app'
            }
        }
    }
}
