pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/Micky23-byte/Django-Ecommerce.git'
            }
        }
        
        stage('Set Up Virtual Environment') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh '''
                . venv/bin/activate
                # Downgrade setuptools for compatibility with older packages
                pip install "setuptools<60" wheel
                # Now install all requirements
                pip install -r requirements.txt
                '''
            }
        }

        stage('Apply Migrations') {
            steps {
                sh '''
                . venv/bin/activate
                python manage.py migrate
                '''
            }
        }

        stage('Run Server') {
            steps {
                sh '''
                . venv/bin/activate
                python manage.py runserver 0.0.0.0:8000
                '''
            }
        }
    }
}
