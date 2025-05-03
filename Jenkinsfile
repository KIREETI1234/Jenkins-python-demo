pipeline {
    agent any

    environment {
        VENV_DIR = '.venv'
    }

    stages {
        stage('Setup') {
            steps {
                echo 'Creating virtual environment and installing dependencies...'
                sh 'python3 -m venv $VENV_DIR'
                sh '. $VENV_DIR/bin/activate && pip install --upgrade pip'
                sh '. $VENV_DIR/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
                echo 'No build step for Python, moving on...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running pytest...'
                sh '. $VENV_DIR/bin/activate && pytest tests/'
            }
        }

        stage('Coverage Report') {
            steps {
                echo 'Generating code coverage report...'
                sh '. $VENV_DIR/bin/activate && coverage run -m pytest tests/'
                sh '. $VENV_DIR/bin/activate && coverage report'
                sh '. $VENV_DIR/bin/activate && coverage html'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
