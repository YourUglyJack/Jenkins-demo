pipeline {
    agent any

    environment {
        VENV = "test/venv"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python') {
            steps {
                sh '''
                python3 -m venv $VENV || true
                source $VENV/bin/activate
                '''
            }
        }

        // stage('Migrate DB') {
        //     steps {
        //         sh '''
        //         source $VENV/bin/activate
        //         python manage.py migrate
        //         '''
        //     }
        // }

        stage('Start Django') {
            steps {
                sh '''
                source $VENV/bin/activate
                pkill -f "manage.py runserver" || true
                nohup python manage.py runserver 0.0.0.0:8000 &
                '''
            }
        }
    }
}
