pipeline {
    agent any

    // tools {
    //     sonarQube 'SonarQube'
    // }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/hienpuzzle/python-ci-cd-pipeline.git'
            }
        }

        stage('Setup Environment') {
            steps {
                echo 'Setting up Python environment...'
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Linting') {
            steps {
                echo 'Running flake8 for linting...'
                sh '. venv/bin/activate && flake8 .'
            }
        }

        stage('Testing') {
            steps {
                echo 'Running pytest for unit tests...'
                sh '. venv/bin/activate && pytest --cov=app --cov-report=xml'
            }
        }

        // stage('SonarQube Analysis') {
        //     steps {
        //         echo 'Running SonarQube analysis...'
        //         withSonarQubeEnv('SonarQube') {
        //             sh '''
        //             . venv/bin/activate
        //             sonar-scanner \
        //               -Dsonar.projectKey=python-ci-cd-pipeline \
        //               -Dsonar.sources=. \
        //               -Dsonar.python.coverage.reportPaths=coverage.xml
        //             '''
        //         }
        //     }
        // }

        stage('Deploy') {
            steps {
                echo 'Deploying Python application...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
