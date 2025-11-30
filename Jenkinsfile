pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Micky23-byte/Django-Ecommerce.git'
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

        stage('Run Tests (Optional)') {
            steps {
                sh '''
                    . venv/bin/activate
                    python manage.py test || true
                '''
            }
        }

        // You can remove this stage if you're deploying instead
        stage('Run Server') {
            steps {
                sh '''
                    . venv/bin/activate
                    python manage.py runserver 0.0.0.0:8000 &
                '''
            }
        }

    }
}
